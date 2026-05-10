tags:: #Logseq #[[Logseq tips]] #[[Claude Sonnet]] #apolloapp #How-to 
source:: [[Claude Sonnet 4]] in [[apolloapp]] by #claudeprompt
parent:: #How-to
- User: Pocket owned by Firefox is going to retire. What are the alternatives for saving articles and recipes? I know there’s Readwise and Readwise Reader but they don’t have a free tier. Instapaper sounds promising. I’m already using Logseq as my knowledge base and often put quotes and my reflections on web articles there. Any other options or should I stick to Logseq? Though I need to come up with a better structure and organisation in Logseq if I were to use it as replace of pocket.
- Assistant: You're right that Pocket is shutting down - [Mozilla announced](https://support.mozilla.org/en-US/kb/future-of-pocket) users have until October 8, 2025 to export their data before it's permanently deleted.
- [Instapaper](https://www.instapaper.com/) is indeed a solid choice. It's been around for ages, syncs across devices (iPhone, iPad, Android, Kindle), works offline, and has a generous free tier. It's quite reliable for the core "save and read later" functionality.
- Other alternatives worth considering:
  **Raindrop.io** - Has excellent organisation with nested collections, tags, and full-text search. The free tier is quite generous and it handles both articles and recipes well.
  **Omnivore** - Open source, completely free, and has good highlighting/annotation features that might complement your Logseq workflow.
  **Matter** - Clean interface with social features, though more limited on the free tier.
- Since you're already invested in Logseq, you could absolutely use it as your primary system. The key would be developing a consistent structure - perhaps something like:
  id:: 68319616-5172-4e34-a33b-314234d5ce9a
	- A dedicated page for "Reading Inbox"
	- Template blocks for articles with metadata (URL, date saved, tags)
	- Clear tagging system to distinguish recipes from articles
	- Regular review process to move items from inbox to permanent notes
- The advantage of staying with Logseq is everything stays in one system where you can easily link articles to your other notes and thoughts. What's your current workflow like for getting web content into Logseq?
- User: Was looking at Omnivore but heard that it’s shutting down. Is it true?
- Assistant: Yes, unfortunately Omnivore is shutting down. The team announced in October 2024 that they were acquired by ElevenLabs, and [techcrunch.com](https://techcrunch.com/2024/10/29/elevenlabs-has-hired-the-team-behind-omnivore-a-reader-app/) reported that the service shut down on November 15, 2024. 
  collapsed:: true
  
  [theverge.com](https://www.theverge.com/2024/10/29/24283055/one-of-my-favorite-read-later-apps-is-shutting-down) mentioned users only had about two weeks to export their data before it went away. The Omnivore team is now working on ElevenLabs' own reader app called ElevenReader, which focuses on text-to-speech functionality.
  
  This makes your timing quite relevant - you're looking for Pocket alternatives just as another popular free option has disappeared. As [molodtsov.me](https://molodtsov.me/2024/10/omnivore-is-dead-where-to-go-next/) noted, Omnivore failed partly because it was free and couldn't sustain itself.
  
  This actually strengthens the case for either Instapaper (which has been around since 2008 and has a sustainable model) or building your own system in Logseq. At least with Logseq, you own your data completely and aren't dependent on external services that might shut down.
  
  What's drawing you to a dedicated read-later app versus just expanding your Logseq workflow?
- User: I’m just looking at my options. I open to expand my Logseq workflow.
- Assistant: That's a sensible approach. Since you're already comfortable with Logseq and have it set up for knowledge management, expanding it could be quite powerful.
  
  Looking at the search results, there's actually a nice example of someone using [Raindrop.io with Logseq](https://reticulated.net/posts/a-better-bookmark-experience-with-raindrop.io-and-logseq/) - they use Raindrop for the initial saving and tagging, then sync it into Logseq for deeper processing and linking. That could be a hybrid approach if you want the convenience of a dedicated bookmark tool but the power of Logseq for your knowledge work.
- For a pure Logseq approach, you might consider:
  id:: 6831964c-35b0-4e09-bd44-5ea2f7116494
  
  **Capture workflow**: Use the web clipper browser extension or simple bookmarklets to quickly save URLs with basic metadata to your daily journal or a dedicated "Inbox" page.
  
  **Structure**: Create templates for different content types (articles vs recipes) and establish consistent tagging - perhaps `#to-read`, `#recipes`, `#articles`, plus topic tags.
  
  **Processing**: Set up a regular review rhythm to move items from your inbox into permanent notes, extract key insights, and create connections to existing content.
- The beauty of Logseq is that your saved articles aren't just sitting in a list - they become part of your broader knowledge network where you can discover unexpected connections.
  
  What parts of your current Logseq setup work well for you, and where do you feel the friction points are?
- User: I don’t think I need an inbox as my reading list. I don’t really use them. So we can skip Raindrop altogether. I already directly capture urls into Logseq and get quotes and highlights under the urls. But I’m thinking should I clip the whole webpage into Logseq or make a new page with just the highlights. I’m more inclined to second approach or something similar as that’s what I’m doing right now.
  collapsed:: true
  My Logseq workflow now:
  1. Create a page if the article is talking about a specific topic 
  2. Capture URL into Logseq
  3. Copy and Paste paragraphs and quotes into Logseq
  4. Add highlights in Logseq
  5. Sometimes add my thoughts
  
  Any room for improvements or streamlining the process or organisation?
- Assistant: Your workflow is already quite solid! You're doing the essential things - capturing the source, extracting key content, and adding your own thinking. Here are some potential refinements:
- **Process improvements:**
  id:: 68319682-79bd-49f5-860f-00b64333def1
	- Consider using a consistent template for articles to speed up step 1. Something simple like `## Source: [URL]`, `## Key Points:`, `## My Thoughts:` could standardise your format
	- For step 3, you might experiment with [MarkDownload browser extension](https://hub.logseq.com/integrations/aV9AgETypcPcf8avYcHXQT/markdownload-a-web-clipper-for-logseq/uvhfmwydMsUZ5Rxdds3wTa) which can clip selected text directly into markdown format, saving some copy-paste effort
- **Organisation tweaks:**
  id:: 68319688-e5a2-41ae-b679-1e1ccb823270
	- Add consistent metadata like `date-read::`, `type:: article/recipe`, or `status:: processed` as properties to help with future queries
	- Consider whether you need both page titles about topics AND the article URLs, or if linking them differently might reduce duplication
	- Use block references for quotes so you can reference specific insights across different pages without duplicating content
- **One question:** When you say "create a page if the article is talking about a specific topic" - are you creating topic pages that aggregate multiple sources, or individual pages per article? That choice affects how you might want to structure the metadata and cross-references.
  
  Your current approach of highlights + your thoughts is definitely the right balance - you're not drowning in full-text but capturing what matters.
- User: Love your suggestions on the tags. Definitely need to improve on that. My metadata organisation is subpar. I will follow your suggestions.
  
  To answer your question, I’m talking about a topic page with different web sources. Do you have any recommendations on this approach?
- Assistant: That's a brilliant approach - topic pages are much more valuable than scattered individual article pages. You're essentially building your own knowledge clusters around subjects you care about.
- **Structure suggestions for topic pages:**
  id:: 6831970b-20e7-4e23-8086-cea3e7ff6843
	- **Page header with metadata:**
	  ```
	  tags:: #concept #domain-name
	  status:: active/developing
	  sources:: 3
	  last-updated:: [[2025-05-24]]
	  ```
	- **Content organisation:**
		- **Overview/Definition** section at the top (your synthesis)
		- **Key Insights** broken down by subtopics
		- **Sources** section with each source as a collapsible block containing:
			- URL and date accessed
			- Key quotes/highlights from that source
			- Your thoughts on that specific source
	- **Cross-linking:**
		- Link freely to other topic pages when concepts overlap
		- Use block references to pull key insights into related pages
		- Tag individual sources within the page for later querying
	- **Maintenance rhythm:**
		- When you find a new source on an existing topic, add it to the existing page rather than creating a new one
		- Periodically review and update your overview section as your understanding develops
		- Split pages that become unwieldy (say, over 20 sources) into more focused subtopics
- This creates a living knowledge base where each topic page becomes increasingly valuable over time. Do you find certain topics naturally clustering together, or do you prefer keeping them quite distinct?
  User: Great this looks like an improved version of what I already have. Now I have a big task to migrate everything to Logseq… 😅
- Assistant: Haha, the classic curse of knowledge management - every time you improve your system, you've got to retrofit everything! 😅
- **Migration sanity tips:**
	- **Don't try to do it all at once** - that's a recipe for burnout. Maybe tackle one topic area per week, or set a timer for 30 minutes and see how much you can reorganise in that time.
	- **Start with your most active topics** - the ones you're still actively reading about. Those will give you the biggest immediate benefit and help you refine your new structure before tackling older material.
	- **Use Logseq's query powers** - you can probably find patterns in your existing content with simple queries like `{{query (page-property :tags concept)}}` to gather related pages together.
	  id:: 683197de-b866-49e4-b6c9-6d97f6635100
	- **Don't aim for perfection** - your old content doesn't need to match your new format exactly. Just getting URLs and key insights into the right topic buckets will be a huge improvement.
	- **Consider this a review opportunity** - you'll probably find outdated content you don't need anymore, or insights that connect in ways you hadn't noticed before.
- At least you're not dealing with Pocket's October deadline while doing this migration! Take your time with it - even a partially improved system is better than perfect paralysis.