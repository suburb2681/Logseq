tags:: #[[Proton Mail]] #Sieve 
parent:: #[[Proton Mail]]
source:: Gemini Pro 2.0 in [[OpenCat app]] with [[Code Assistant]] prompt
- Okay, here is a Sieve rule for Proton Mail that should accomplish your goal.
  
  **Important Considerations:**
  
  1.  **Applies to Incoming Mail:** Standard Sieve rules in Proton Mail run *when an email arrives*. They don't automatically run retroactively on your entire mailbox history. This rule will archive *newly arriving* emails that meet the criteria (i.e., they were *sent* over a year ago but are just arriving now, perhaps due to forwarding or mailing list delays) or emails that are processed by Sieve for other reasons (like manual filter application, if Proton Mail supports that). It won't automatically clean up your existing folders unless Proton Mail offers a way to manually trigger Sieve rules on existing mail.
  2.  **Label Name:** Ensure your label is *exactly* named `important` (case-sensitive might matter depending on implementation, though label matching is often case-insensitive). If your label is named differently (e.g., "Important", "!Important"), adjust the script accordingly.
  3.  **`received` vs `date` header:** This script uses the `received` date, which reflects when Proton Mail's servers received the email. This is generally more reliable than the `Date:` header within the email, which can sometimes be incorrect or manipulated.
  4.  **Proton Mail Specific Extension:** This uses `vnd.proton.labels`, which is specific to Proton Mail.
  
  ```sieve
  require ["include", "environment", "variables", "relational", "comparator-i;ascii-numeric", "spamtest", "fileinto", "vnd.proton.expire", "date", "vnd.proton.labels", "editheader", "duplicate", "mailbox", "subaddress"];
  
  # Rule: Archive emails older than 1 year unless tagged 'important'
  
  # Check if the email was received more than 1 year ago
  # AND if it does NOT have the 'important' label
  if allof (
      date :value "ge" :originalzone "received" "1y",  # ":value 'ge'" means "greater than or equal to" 1 year ago
      not haslabel "important"                         # Check if the 'important' label is NOT present
  )
  {
      # If both conditions are true, move the email to the Archive folder
      fileinto "Archive";
  
      # Stop processing further rules for this email
      stop;
  }
  
  # If the email didn't match the rule above,
  # it continues to be processed by any subsequent rules or default delivery.
  ```
  
  **Explanation:**
  
  1.  `require [...]`:** This line declares all the Sieve extensions the script *might* use. While not all are strictly needed for *this specific rule*, including the standard Proton Mail set is safe practice. The essential ones here are `fileinto`, `date`, `vnd.proton.labels`, `relational`, and `comparator-i;ascii-numeric`.
  2.  `if allof (...)`:** This means *all* conditions listed inside the parentheses must be true for the actions inside the `{...}` block to be executed.
  3.  `date :value "ge" :originalzone "received" "1y"`:**
      *   `date`: Invokes the date comparison test.
      *   `:value "ge"`: Uses the `relational` extension to check if the date value is "greater than or equal to" the specified duration in the past.
      *   `:originalzone`: Ensures timezones are handled correctly based on the original reception time.
      *   `"received"`: Specifies that the comparison should be based on when the email was *received* by the server.
      *   `"1y"`: Represents the duration of "1 year". So, this checks if the received date is 1 year ago or older.
  4.  `not haslabel "important"`:**
      *   `haslabel "important"`: Uses the Proton Mail specific extension `vnd.proton.labels` to check if the email has the label named "important".
      *   `not`: Negates the result. So, this condition is true only if the email *does not* have the "important" label.
  5.  `fileinto "Archive";`:** If both conditions in the `allof` are met, this action moves the email to your standard Archive folder.
  6.  `stop;`:** This command tells the Sieve interpreter to stop processing any further rules for this particular email. This is important to prevent other rules from potentially acting on an email you've already decided to archive.
  
  **How to Add this Rule in Proton Mail:**
  
  1.  Go to Settings -> Go to settings -> Filters -> Custom filters.
  2.  Click "Add Sieve filter".
  3.  Give your filter a name (e.g., "Archive Old Mail").
  4.  Paste the entire Sieve script provided above into the text box.
  5.  Click "Save".
  
  Remember the limitation about this applying primarily to *incoming* mail processed by the Sieve filter.