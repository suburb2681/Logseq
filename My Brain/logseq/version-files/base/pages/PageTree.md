- ```javascript
  // PageTree
  
  PageTree = logseq.kits.PageTree = {
      children: { queries: {}, titles: {} },
      max: {},
      roots: { queries: {}, titles: {} }
  };
  
  PageTree.configFromDiv = function configFromDiv(div){
      const nodeprop = div.dataset.nodeProp;
      if (!nodeprop) return;
  
      delete div.dataset.nodeProp;
  
      const leafprep = div.dataset.leafPrep;
      const leafprop = div.dataset.leafProp;
      const leafconfig = {
          prep: (leafprep !== "$3") && leafprep,
          prop: (leafprop !== "$4") && leafprop,
          not: leafprop === "refs" && leafprep === "is" && nodeprop
      };
  
      const nodeconfig = {
          prep: div.dataset.nodePrep,
          prop: nodeprop
      };
      return {leaf: leafconfig, node: nodeconfig};
  }
  logseq.kits.pagetree = function PageTreeHandler(div){
      const config = PageTree.configFromDiv(div);
      if (!config) return;
  
      const nodeconfig = config.node;
      const pgRoots = PageTree.roots;
      div.textContent = pgRoots.getTitle(nodeconfig);
      const roots = pgRoots.get(nodeconfig);
  
      const nofRoots = roots.length;
      const buttonHandler = nofRoots && function(e){
          e.preventDefault();
          e.stopPropagation();
          PageTree.toggleChildren(button);
      }
      const button = PageTree.button((nofRoots) ? "-" : "Ø", buttonHandler);
      div.prepend(button);
  
      PageTree.filler(config, div, roots, PageTree.max.depth);
  }
  
  // Elements
  
  PageTree.link = function pageLink(name, originalName){
      const a = document.createElement("a");
      a.classList.add("page-ref");
      a.href = "#/page/" + encodeURIComponent(name);
      a.textContent = originalName;
      return a;
  }
  
  PageTree.button = function treeButton(textContent, clickHandler){
      const button = document.createElement("button");
      button.classList.add("tree-button");
      button.textContent = textContent;
      if (clickHandler) button.addEventListener("click", clickHandler);
      return button;
  }
  
  PageTree.toggleChildren = function toggleChildren(button){
      const isExpanded = (button.textContent === "-");
      button.textContent = (isExpanded) ? "+" : "-";
  
      const newStyle = (isExpanded) ? "none" : "block";
      Array.prototype.forEach.call(button.parentElement.children, (child)=>{
          if (child.className === "pagetree-node") child.style.setProperty("display", newStyle);
      });
  }
  
  PageTree.node = function treeNode(button, link){
      const div = document.createElement("div");
      div.classList.add("pagetree-node");
      div.append(button, link);
      return div;
  }
  
  // Fillers
  
  PageTree.fillMore = function fillMoreChildDivs(config, divParent, children, items, child, isItemsNode, depth){
      if (items.length) PageTree.filler(config, divParent, [{items, page: child}], depth);
      PageTree.filler(config, divParent, children, (isItemsNode) ? -1 : depth);
  }
  
  PageTree.filler = function fillChildDivs(config, divParent, children, depth){
      children.forEach( (child)=>{
          const page = child.page;
          const isItemsNode = (page) ? true : false;
          const childName = (isItemsNode) ? page["original-name"] : child["original-name"];
          const leafconfig = config.leaf;
  
          const getChildren = PageTree.children.get;
          const items = (leafconfig.prop && !isItemsNode && depth > 0) ? getChildren(leafconfig, childName) : [];
          const nofItems = items.length;
          const children = (depth < 0) ? [] : (isItemsNode) ? child.items : getChildren(config.node, childName);
          const nofChildren = children.length + (nofItems ? 1 : 0);
  
          const newDepth = depth - 1;
          const small = (newDepth > 0 && nofChildren <= PageTree.max.siblings);
  
          const buttonText = (nofChildren) ? ((small) ? "-" : "...") : " ";
          const buttonHandler = nofChildren && function(e){
              e.preventDefault();
              e.stopPropagation();
  
              if (button.textContent === "...") PageTree.fillMore(config, divChild, children, items, child, isItemsNode, PageTree.max.depth);
              PageTree.toggleChildren(button);
          };
          const button = PageTree.button(buttonText, buttonHandler);
  
          const link = (isItemsNode) ? PageTree.children.getTitle(leafconfig) : PageTree.link(child.name, childName);
          const divChild = PageTree.node(button, link);
          if (nofChildren && small) PageTree.fillMore(config, divChild, children, items, child, isItemsNode, newDepth);
          divParent.append(divChild);
      });
  }
  
  // Getters
  
  PageTree.getData = function getData(query, ...inputs){
      const res = logseq.api.datascript_query(query, ...inputs);
      return res.flat().sort( (a, b)=>{ return a.name.localeCompare(b.name) } );
  }
  
  PageTree.children.get = function getChildren(config, parent){
      const query = PageTree.children.queries[(config.not) ? "refs" : config.prep];
      return PageTree.getData(query, ":" + (config.not || config.prop), `"${parent.toLowerCase()}"`);
  }
  PageTree.children.getTitle = function getTitle(config){
      const prep = (config.not) ? "refs" : config.prep;
      return PageTree.children.titles[prep].replace("leafprop", config.prop);
  }
  
  PageTree.roots.get = function getRoots(config){
      const query = PageTree.roots.queries[config.prep];
      return PageTree.getData(query, ":" + config.prop);
  }
  PageTree.roots.getTitle = function getTitle(config){
      return PageTree.roots.titles[config.prep].replace("nodeprop", config.prop);
  }
  
  // Queries
  
  PageTree.children.queries.refs = `[
      :find (pull ?Child [*])
      :in $ ?prop ?Parent-name
      :where
          [?child :block/page ?Child]
          [?child :block/refs ?Parent]
          [?Parent :block/name ?Parent-name]
          [?Parent :block/original-name ?Parent-original-name]
          (not 
              [?child :block/properties ?child-props]
              [(get ?child-props ?prop) ?child-from]
              [(contains? ?child-from ?Parent-original-name)]
          )
  ]`;
  PageTree.children.queries.from = `[
      :find (pull ?Child [*])
      :in $ ?prop ?Parent-name
      :where
          [?child :block/page ?Child]
          [?child :block/properties ?child-props]
          [(get ?child-props ?prop) ?child-from]
          [?Parent :block/name ?Parent-name]
          [?Parent :block/original-name ?Parent-original-name]
          [(contains? ?child-from ?Parent-original-name)]
  ]`;
  PageTree.children.queries.to = `[
      :find (pull ?Child [*])
      :in $ ?prop ?Parent-name
      :where
          [?Parent :block/name ?Parent-name]
          [?parent :block/page ?Parent]
          [?parent :block/properties ?parent-props]
          [(get ?parent-props ?prop) ?parent-to]
          [?Child :block/original-name ?Child-original-name]
          [(contains? ?parent-to ?Child-original-name)]
  ]`;
  PageTree.children.queries.has = PageTree.children.queries.to;
  PageTree.children.queries.is = PageTree.children.queries.from;
  
  PageTree.roots.queries.from = `[
      :find (pull ?Root [*])
      :in $ ?prop
      :where
          [?child :block/properties ?child-props]
          [(get ?child-props ?prop) ?child-from]
          [?Root :block/original-name ?Root-original-name]
          [(contains? ?child-from ?Root-original-name)]
          (not
              [?root :block/page ?Root]
              [?root :block/properties ?root-props]
              [(get ?root-props ?prop) ?root-from]
          )
  ]`;
  PageTree.roots.queries.to = `[
      :find (pull ?Root [*])
      :in $ ?prop
      :where
          [?root :block/page ?Root]
          [?root :block/properties ?root-props]
          [(get ?root-props ?prop) ?root-to]
          (not 
              [?parent :block/properties ?parent-props]
              [(get ?parent-props ?prop) ?parent-to]
              [?Root :block/original-name ?Root-original-name]
              [(contains? ?parent-to ?Root-original-name)]
          )
  ]`;
  
  // Settings
  
  PageTree.max.depth = 16;
  PageTree.max.siblings = 16;
  
  PageTree.roots.titles.from = "Tree from nodeprop:"
  PageTree.roots.titles.to = "Tree to nodeprop:"
  PageTree.children.titles.is = "is in leafprop of:"
  PageTree.children.titles.has = "has leafprop:"
  PageTree.children.titles.refs = "is referred by:"
  ```
- source:: **15:47** [[quick capture]]:  https://discuss.logseq.com/t/generate-explicit-hierarchy-out-of-properties/20635
  tags:: #Logseq
  exclude-from-graph-view:: true
-