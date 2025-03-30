tags:: [[Proton Mail]]
parent:: #[[Proton Mail]]
source:: Gemini Pro 2.0 in [[OpenCat app]] with [[Code Assistant]] prompt

- You've hit on a key limitation of server-side filtering like Sieve in most email systems, including Proton Mail: **Sieve rules typically run *only* when a message arrives at the server.** They generally don't have a built-in mechanism to automatically scan and act upon emails already stored in your folders.
  
  So, Proton Mail itself does not currently offer a built-in, automatic way to run rules (like your Sieve filter) retroactively across your entire existing mailbox *on the server side*.
  
  However, you do have a few options, ranging from manual to potentially more automated using external tools:
  
  1.  **Manual Archiving using Search (Proton Mail Web/Apps):**
      *   This is the most straightforward, built-in method, but it's manual.
      *   **How:**
          *   Go to the Proton Mail web interface or use a desktop/mobile app.
          *   Use the search bar. You can search by date. The syntax might be something like `before:YYYY/MM/DD` or use the advanced search dropdowns. For example, to find emails older than one year (from today, say June 11, 2024), you'd search for `before:2023/06/11`.
          *   **Crucially:** You also need to exclude the 'important' label. You might need to combine search terms or perform the search within specific folders *that do not include* items labeled 'important'. Searching for emails *without* a specific label can sometimes be tricky depending on the interface. An alternative is to search *all* old emails (`before:2023/06/11`) and then *manually deselect* any marked 'important' before archiving.
          *   Select the emails found by the search (often there's a "select all" option for the search results).
          *   Click the "Archive" button.
      *   **Downside:** You need to remember to do this periodically (e.g., once a month, once a year). It's not automatic.
  
  2.  **Proton Mail Bridge + Desktop Email Client (e.g., Thunderbird, Outlook):**
      *   This is the most likely way to achieve *semi-automation* for existing emails.
      *   **How:**
          *   Install and configure the [Proton Mail Bridge](https://proton.me/mail/bridge). This application runs on your computer and decrypts/encrypts your mail locally, allowing you to use standard desktop email clients.
          *   Configure a desktop email client like Thunderbird or Outlook to access your Proton Mail account via the Bridge.
          *   Most desktop clients have much more powerful filtering capabilities that *can* be run on existing folders. In Thunderbird, for example, you can create a "Filter" (similar to a rule) with conditions like "Date is before [1 year ago]" AND "Tags isn't 'important'" (Proton Mail labels often map to 'tags' in clients like Thunderbird).
          *   You can then manually trigger this filter to run on specific folders or even your entire account (Tools -> Run Filters on Folder). Some clients might even allow scheduling this, but often it still requires the client to be running.
      *   **Downsides:**
          *   Requires installing and running the Bridge and a desktop client.
          *   The processing happens on *your computer*, not Proton Mail's servers. Your computer needs to be on and the client running for the rules to execute.
          *   Depending on mailbox size, downloading headers or full messages to the client can take time and disk space.
          *   Mapping Proton Mail labels exactly to client tags/categories might need careful checking.
  
  3.  **Proton Mail Expiration Feature (Deletion, Not Archiving):**
      *   Proton Mail *does* have a feature for emails to automatically expire (be deleted) after a certain time. This can be set via Sieve (`vnd.proton.expire`) for incoming mail or manually on specific emails/conversations.
      *   **Downside:** This *deletes* emails permanently (moves them to Trash first, then permanently deletes based on your Trash settings), it does *not* archive them. This doesn't match your requirement.
  
  **In summary:**
  
  *   **No built-in automatic server-side retroactive archiving.**
  *   **Best built-in option:** Periodic manual search and archive via web/app.
  *   **Best semi-automated option:** Use Proton Mail Bridge with a desktop client (like Thunderbird) that can run filters on existing folders locally.
  
  For most users, the periodic manual search is the simplest approach, though less convenient than true automation. The Bridge option offers more power but comes with added complexity.