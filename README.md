gow -e go,html,js,json run .
npm run cypress

gow test -short -cover ./...
go clean -testcache
go test  -cover -short ./... -coverprofile cover.out  && go tool cover -html cover.out -o cover.html && open cover.html


go vet ./...


# heroku commands
```bash
git push heroku main:main
heroku logs --tail

modd // to automatically run test when change file


# Test
npx cypress open


# déploiement héroku
       
remote:        Installed the following binaries:
remote:                 ./bin/accuweather
remote:                 ./bin/twi
remote:        
remote:        Created a Procfile with the following entries:
remote:                 twi: bin/twi
remote:                 accuweather: bin/accuweather
➜  twi git:(main) heroku ps
No dynos on ⬢ rossypro-twi
➜  twi git:(main) heroku ps:scale twi=1
Scaling dynos... done, now running twi at 1:Basic



alias cy="npx cypress open"
alias tc="go test -coverprofile cover.out ./... && go tool cover -html=cover.out"
alias lc='grep -v -e " 1$" cover.out'


Twillio code exchange for sms
https://www.twilio.com/code-exchange?q=&f=sms&utm_source=drip&utm_medium=email&utm_campaign=Onboarding&utm_content=GRTH_NRTR_2022_Twilio_Onboarding_NAMER_Onboarding_SMS_Email_4_10641&utm_term=0&mkt_tok=Mjk0LVRLQi0zMDAAAAGWBnhOefl36IijKts8TS3E9EUObh30w0zWKm-cA6Skg0GZu_bh2USC-sacNGIAi_uZCSdwfFo2oOBxhY10aRtkrNNxkiOetpmgXfecoj6hM_EuXV3E


# Use cases
Here’s a breakdown of the use cases for the SMS messaging service you're building. I've added the main use cases you requested and a few missing ones that would help ensure full functionality.

---

### **Use Case 1: User Account Creation**

- **Actor:** New User
- **Precondition:** User sends an initial SMS to the service.
- **Trigger:** The first time a user interacts with the service.
  
#### **Main Flow:**
1. **System prompts** the user to provide an email address and a secondary phone number (optional, especially if supporting WhatsApp).
2. User responds with their **email address** and **secondary phone number** (if they have WhatsApp).
3. **System validates** the email and phone numbers.
4. If valid, the **system creates the user account** and sends a confirmation SMS.
5. If not valid, the **system sends an error message** asking the user to retry.

#### **Extensions:**
- **Invalid email/phone:** System requests correct information again.
- **User cancels:** User can send a "cancel" message to abort the process.

---

### **Use Case 2: Add Credit to User Account**

- **Actor:** Existing User
- **Precondition:** User must have an existing account.
- **Trigger:** User sends an SMS to request adding credit.
  
#### **Main Flow:**
1. **User sends SMS** with the keyword “Add Credit” or similar.
2. **System prompts** user to select an amount or type in the amount to add (e.g., $10, $20, etc.).
3. User replies with the amount.
4. **System verifies** the amount and **prompts for payment method** (e.g., SMS, credit card, etc.).
5. User provides payment information.
6. **System processes payment** and adds the credit to the user account.
7. **System sends confirmation** SMS with updated account balance.

#### **Extensions:**
- **Payment failure:** System informs the user of failure and retries.
- **Low balance warning:** The system could periodically warn the user when their credit is low.

---

### **Use Case 3: Make Google Search Engine Request**

- **Actor:** Existing User
- **Precondition:** User has enough credit in their account.
- **Trigger:** User sends an SMS to perform a Google search.

#### **Main Flow:**
1. **User sends SMS** with the keyword “Search” followed by the search query (e.g., “Search best pizza places in NYC”).
2. **System validates** that the user has enough credit.
3. **System performs the search** on Google and retrieves the top result(s).
4. **System sends SMS** back to the user with the top search result(s) (e.g., title, brief description, and URL).
5. System **deducts credit** from the user’s account.

#### **Extensions:**
- **Insufficient credit:** The system informs the user and provides options to add credit.

---

### **Use Case 4: Make AI Chat Call**

- **Actor:** Existing User
- **Precondition:** User has enough credit in their account.
- **Trigger:** User sends an SMS to initiate a conversation with an AI chatbot.

#### **Main Flow:**
1. **User sends SMS** with the keyword “Chat” followed by the query (e.g., “Chat What is the weather like today in Paris?”).
2. **System validates** that the user has enough credit.
3. **System sends the query** to the AI chatbot and retrieves a response.
4. **System sends SMS** back to the user with the AI’s response.
5. System **deducts credit** from the user’s account.

#### **Extensions:**
- **Long responses:** If the AI response exceeds SMS length, the system may send multiple SMS messages.
- **Insufficient credit:** The system informs the user and provides options to add credit.

---

### **Use Case 5: Check Balance**

- **Actor:** Existing User
- **Precondition:** User has an account.
- **Trigger:** User sends an SMS to check their account balance.
  
#### **Main Flow:**
1. **User sends SMS** with the keyword “Balance.”
2. **System retrieves current balance** for the user.
3. **System sends SMS** back to the user with the current balance.

---

### **Use Case 6: Receive Daily Summary of Available Credit**

- **Actor:** Existing User
- **Precondition:** User has an account.
- **Trigger:** System sends a daily SMS with a summary of the user’s available credit.

#### **Main Flow:**
1. **System checks** the user’s account balance at a scheduled time (e.g., once a day).
2. **System sends SMS** to the user with their current credit balance.

#### **Extensions:**
- **Low balance alert:** System could also send a low balance notification as part of the summary.

---

### **Use Case 7: Edit Account Information (Email/Phone)**

- **Actor:** Existing User
- **Precondition:** User has an account.
- **Trigger:** User sends an SMS requesting to update their account details (email or phone).

#### **Main Flow:**
1. **User sends SMS** with the keyword “Update” and specifies the new information (e.g., new email address or phone number).
2. **System verifies** the new email or phone number.
3. **System updates** the account with the new information and confirms the change via SMS.

#### **Extensions:**
- **Invalid input:** System asks the user to re-enter valid information.

---

### **Use Case 8: Help / Support Request**

- **Actor:** User (New or Existing)
- **Precondition:** User may or may not have an account.
- **Trigger:** User sends an SMS requesting help or support.

#### **Main Flow:**
1. **User sends SMS** with the keyword “Help” or “Support.”
2. **System responds** with a list of supported keywords and a short description of each (e.g., Add Credit, Search, Chat, Balance, Update, etc.).
3. If the issue persists, the **system provides a support phone number or email** for further assistance.

---

### **Missing Use Cases:**

1. **User Authentication via SMS Code (Optional)**
   - The system can send an SMS code for verification when a new account is created or when sensitive changes (like adding credit) are made.

2. **Deactivate Account**
   - Users may want to deactivate their account via SMS if they no longer wish to use the service.

3. **Refund/Dispute Handling**
   - If a payment fails or there’s an issue with service access, a use case can handle refund or dispute resolution via SMS.

4. **Request Service History (Search/Chat)**
   - Users may want to request a summary of their recent searches or AI chat interactions.

SMS Payment Links:
Instead of asking users to enter credit card details via SMS, send them a secure link to a payment portal where they can enter their payment information safely. This method is more secure and compliant with regulations.# www.twai-sms-server
