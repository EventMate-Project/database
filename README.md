# database

### 5. **Orders**

* **Description:** Handles transactions of ticket purchases.
* **Fields:**

  * `id`: Unique id of order
  * `customerId`: Unique id of user who made the order
  * `eventId`: Id of the event for which the tickets were purchased 
  * `tickets` (array of ticket IDs): Productos adquiridos
  * `totalPrice` : Total Price
  * `paymentStatus` (pending, paid, failed, refunded) : Actual state of the payment
  * `createdAt`: Date it was created

👉 **Business role:** Allows tracking of purchases separate from tickets (important for audits and refunds).

---

### 6. **Subscriptions**

* **Description:** Tracks organizer subscription plans (for monetization phase).
* **Fields:**

  * `id`: Unique id of the subscription
  * `organizerId`: Id of the organizer
  * `planName`: Name of the plan the organizar is subscribed
  * `price`: Price of the subscription
  * `start`, `end` : Start and end dates of the subscription acquired
  * `status` (active, canceled, expired): State of the subscription

👉 **Business role:** Future monetization channel (e.g., premium analytics, lower commission fees).

---

### 7. **Notifications**

* **Description:** Represents system-generated messages sent to users or organizers.
* **Fields:**

  * `id`: Unique id of Notification
  * `recipientId` (customer or organizer): Id of the recipient
  * `eventId` (optional, e.g., event updates): Id of the event, in case was an event update
  * `type` (reminder, update, promo): Type of the notification
  * `title`, `detail`: Information about the notification
  * `sentAt`: Time it was sent
  * `read` (bool): If it was read. 

👉 **Business role:** Improves user engagement and event communication.

---

### 8. **Favorites (optional separate collection or embedded in User)**

* **Description:** Stores user preferences for quick access.
* **Fields:**

  * `id`: Unique id of the favorite item
  * `customerId`: Id of the user 
  * `eventId`: Event that was selected
  * `savedAt`: Time it was saved
