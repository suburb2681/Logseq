tags:: [[Proton Mail]] #Sieve
parent:: #[[Proton Mail]]
source:: Gemini Pro 2.0 in [[OpenCat app]] with [[Code Assistant]] prompt
- Okay, here is a Sieve script for Proton Mail that allows you to set an expiration date (automatic deletion) for emails based on sender or recipient addresses. You can easily edit the list of addresses and the expiration duration directly within the script.
  
  **Important:**
  *   **Expiration = Deletion:** This rule will move emails to the **Trash** folder after the specified duration. They will then be permanently deleted according to your Trash emptying settings (e.g., after 30 days in Trash). This is **different from archiving**.
  *   **Applies to Incoming Mail:** Like the previous rule, this runs when emails *arrive*. It won't retroactively apply expiration to emails already in your mailbox.
  *   **Case-Insensitive:** The `:is` comparator used for addresses is typically case-insensitive.
  
  ```sieve
  require ["include", "environment", "variables", "relational", "comparator-i;ascii-numeric", "spamtest", "fileinto", "vnd.proton.expire", "date", "vnd.proton.labels", "editheader", "duplicate", "mailbox", "subaddress", "address"];
  
  # ========================================
  # == Configuration Section ==
  # ========================================
  
  # 1. Define the list of email addresses to apply expiration to.
  #    - Add or remove addresses within the square brackets [ ... ].
  #    - Each address must be in double quotes " " and separated by a comma ,
  #    - This example checks the SENDER ('From' header). See below for checking recipients.
  define "addresses_for_expiration" [
      "newsletter@example.com",
      "promotions@example.net",
      "no-reply@service.org",
      "social-alerts@example-social.com"
      # Add more SENDER addresses here
  ];
  
  # 2. Define the expiration duration.
  #    - "d" for days, "w" for weeks, "m" for months (approx 30 days), "y" for years.
  #    - Examples: "30d", "8w", "6m", "1y"
  #    - Emails matching the addresses above will be moved to Trash after this period.
  define "expiration_duration" "90d"; # <-- Set your desired duration here (e.g., 90 days)
  
  # ========================================
  # == Rule Logic ==
  # ========================================
  
  # --- Option A: Expire based on SENDER ('From' address) ---
  # (This is active by default with the list defined above)
  if address :is :all "from" ${addresses_for_expiration}
  {
      expire ${expiration_duration};
  
      # Optional: uncomment the 'stop;' line if you want emails matching
      # this rule to NOT be processed by any subsequent Sieve rules.
      # stop;
  }
  
  
  # --- Option B: Expire based on RECIPIENT ('To', 'Cc', 'Bcc' address) ---
  # If you want to expire emails sent TO specific addresses (like your aliases)
  # instead of based on the sender, comment out the 'Option A' block above
  # (put /* before 'if' and */ after the closing '}'), define a new list
  # of your recipient addresses, and uncomment the block below.
  /*
  define "recipient_addresses_for_expiration" [
      "my-special-alias@mydomain.com",
      "receipts@mydomain.com"
      # Add more RECIPIENT addresses here
  ];
  
  if address :is :all ["to", "cc", "bcc"] ${recipient_addresses_for_expiration}
  {
      expire ${expiration_duration}; # Uses the same duration defined above
      # stop;
  }
  */
  
  # --- End of Expiration Rule ---
  # Emails not matching the active rule continue processing.
  ```
  
  **Explanation:**
  
  1.  **`require [...]`:** Includes necessary Sieve extensions, notably `vnd.proton.expire` for setting expiration and `address` for checking email headers, and `variables` for `define`.
  2.  **Configuration Section:** This is where you make your changes.
      *   `define "addresses_for_expiration" [...]`:** Creates a list variable holding the email addresses you want to target. **Edit the content inside the square brackets `[...]`** to add or remove senders.
      *   `define "expiration_duration" "90d";`:** Creates a variable for the duration. **Edit `"90d"`** to your desired timeframe (e.g., `"30d"`, `"6m"`, `"1y"`).
  3.  **Rule Logic:**
      *   **Option A (Sender - Active by default):**
          *   `if address :is :all "from" ${addresses_for_expiration}`: Checks if the full (`:all`) sender address (`"from"`) exactly matches (`:is`, case-insensitive) any address in the `${addresses_for_expiration}` list variable.
          *   `expire ${expiration_duration};`: If there's a match, this command flags the email to be moved to Trash after the duration stored in `${expiration_duration}`.
          *   `stop;` (Optional): If uncommented, prevents further rules from running on this email.
      *   **Option B (Recipient - Inactive by default):**
          *   This block is commented out using `/* ... */`. To use it, you would remove the `/*` and `*/`, potentially define a `${recipient_addresses_for_expiration}` list, and comment out Option A.
          *   `if address :is :all ["to", "cc", "bcc"] ...`: This checks if any of the recipient addresses match the specified list.
  
  **How to Use:**
  
  1.  Go to Proton Mail Settings -> Go to settings -> Filters -> Custom filters.
  2.  Click "Add Sieve filter".
  3.  Give it a name (e.g., "Expire Newsletters").
  4.  **Carefully edit the Configuration Section** in the code above to include the specific sender addresses you want and set your desired expiration duration.
  5.  Paste the *entire edited* Sieve script into the text box.
  6.  Click "Save".
  
  Now, new emails arriving from the senders you listed will automatically be set to expire after the duration you specified.