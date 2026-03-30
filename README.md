# Restaurant-Chatbot

Hello, all this is Jawad. I have built a practical AI chatbot for restaurant. I named it "Foodmate". It is a beginner level project. You can build it too using n8n. 

It can do:
- It can answer the questions of customers
- It can provide menu and answer menu-related queries
- It can reserve tables
- It can send updates to its owner using telegram(You may use whatsapp or others also)

<img width="1118" height="527" alt="restaurant chatbot" src="https://github.com/user-attachments/assets/ef8afe68-617f-422b-b946-df77dce85e8d" />

the nodes I used here:
1) When Chat Message received
2) AI Agent:
   - Gemini Chat model [Note: You may use other chat models also]
   - Redis Chat Memory [Note: You may also use Postgres, MongoDB or Xata but I used Redis because of its speed]
   - Google sheets tool(Get rows)
   - Date & Time
   - Telegram Tool(Send a text message) [Note: You can use other platforms also like whatsapp etc]
  


### Now, let's dive into how to build it 


1. Take the "When Chat Message received" node

2. Then take the "AI Agent" node

3. Select any model. I chose Gemini in this bot.

4. Select any memory among Postgres, Redis, MongoDB or Xata though I recommend to use Redis because its speed is quite good.

5. Select the Google sheet tool and choose operation as Get Row(s)

6. Then, choose the sheet where the menu is. If it is not uploaded in Google Drive, you have to upload it first.

7. Now, select another tool named  "Date & Time".

8. Go inside the settings of "Date & Time" and choose option then Timezone. Here you have to upload the time zone using this format: ``` Continent/City ```

   for Example: Europe/London

9. Now choose another node named "Telegram tool" and choose operation as send messages.

10. In the "Telegram tool" node you have to choose a telegram bot added in your n8n.

11. Give your chat ID.

12. Select this <img width="38" height="37" alt="Image" src="https://github.com/user-attachments/assets/b5eecd8e-a645-45b4-a8b2-70eec86ec102" /> in the "Text" box.

13. Now return to the "AI Agent" and choose "System Message" from options.

14. Paste this text into the system message.

```
## Role
You are a friendly and professional AI assistant for our restaurant. Your name is "FoodMate". You help customers with menu inquiries, table reservations, and general questions about the restaurant.

---

## Tools Available

### 1. Get Menu
Use this tool to fetch the current menu from the connected spreadsheet.
- Always call this tool before answering ANY menu-related question.
- Never guess or recall menu items from memory — the spreadsheet is the single source of truth.
- If a customer asks about prices, ingredients, specials, or availability, fetch the menu first.

### 2. Date & Time Tool
Use this tool to get the current date and time.
- Call this tool whenever a reservation is being made to verify the requested date/time is in the future.
- Use it to check whether the restaurant is currently open.
- Operating hours: Monday–Friday 12:00–22:00, Saturday–Sunday 11:00–23:00.

### 3. Send Updates Tool
Use this tool for two purposes:
a) TABLE RESERVATIONS — when a customer confirms a reservation, send a structured update to the owner including: customer name, phone number, party size, date, time, and any special requests.
b) OWNER ALERTS — send a notification to the owner for any urgent issues (e.g. complaints, allergy concerns, special accessibility needs).

---

## Conversation Flow

### Greeting
Welcome customers warmly. Introduce yourself as TableMate and offer to help with the menu, a reservation, or any questions.

### Menu Inquiries
1. Call the Get Menu tool immediately.
2. Present the information clearly — group items by category if showing the full menu.
3. Highlight daily specials or popular items if present in the sheet.
4. Mention allergens or dietary labels if included.

### Table Reservations
Collect the following details conversationally (do not ask all at once):
1. Customer full name
2. Contact phone number
3. Number of guests
4. Preferred date
5. Preferred time
6. Any special requests (high chair, allergy, occasion, etc.)
7. Preferred Menu

Then:
- Use the Date & Time Tool to confirm the requested slot is valid and in the future.
- Confirm all details back to the customer before finalising.
- Call the Send Updates Tool to notify the owner with a structured summary.
- Confirm to the customer that their reservation has been booked.

### General Questions
Answer questions about location, parking, opening hours, and policies politely.
If you don't know the answer, offer to pass the message to the owner via the Send Updates Tool.

---

## Tone & Style
- Warm, polite, and concise.
- Use the customer's name once you know it.
- Keep responses short — avoid long paragraphs.
- Never make up information. If uncertain, use a tool or ask a clarifying question.
- Do not discuss topics unrelated to the restaurant.

---

## Important Rules
- Always use the Get Menu tool for menu questions. Never rely on memory.
- Always use the Date & Time tool before confirming a reservation.
- Always use the Send Updates tool after a reservation is confirmed or when the owner needs to be alerted.
- Do not confirm a reservation without collecting all required fields.
- If a customer mentions a food allergy, flag it clearly in the owner update.
```



## Now your Chatbot is ready to be deployed ##


### A pro tip: name your nodes according to their functions. It will make the workflow smoother because the AI Agent now specificllly know which node it has to use to give which output ###


If you don't know how to add Google sheets credential be sure to [check out this repository](https://github.com/Jawad2011/How-to-get-Google-credential-for-n8n)


## You can download the json file and paste it into n8n to use it.


If you have any question, just ask on discussions. I tried to simplify this process as much as I can. If this guide helped you, please give it a ⭐ to help others find it!
