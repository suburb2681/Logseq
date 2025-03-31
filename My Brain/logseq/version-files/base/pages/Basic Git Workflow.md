tags:: #Git #Coding, #How-to 
parent:: #Git, #How-to
- ```git
  # Initialize a new repository
  git init
  
  # Add your remote origin (replace with your actual repo URL)
  git remote add origin https://github.com/username/repository.git
  
  # Add all files
  git add .
  
  # Commit
  git commit -m "Your commit message"
  
  # Push changes
  git push -u origin main  # Use 'master' instead of 'main' for older repos
  ```