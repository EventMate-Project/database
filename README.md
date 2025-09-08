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
=======
# Database dictionary

### Customers
- **Description:** Represents attendees (consumers) who register, browse, and purchase tickets.
- **Fields:**
    - ``id``
    - ``name``, ``lastname``
    - ``email``, ``phone``
    - ``age``
    - ``password``
    - ``address`` (embedded: city, district, country)
    - ``favorites`` (array of event IDs or embedded short refs)
    - ``createdAt``, ``updatedAt``

**Business role:** Core actor in the B2C flow. Holds account data and their relationship to events (favorites, tickets purchased).

### Organizers
- **Description:** Represents entities (people, companies, venues) that create and manage events.
- **Fields:**
    - ``id``
    - ``name``
    - ``email``, ``phone``
    - ``password``(hashed)
    - ``subscription`` (array of subscriptions: price, name, start, end, status)
    - ``events`` (array of event IDs they manage)
    - ``createdAt``, ``updatedAt``
**Business role:** Event publishers. Can have free or premium subscriptions in future.

### Events
- **Description:** The main aggregate for any event created by organizers.
- **Field:**
    - ``id``
    - ``title``
    - ``description``
    - ``category`` (concert, conference, sports, etc)
    - ``address`` (embedded: city, district, country, venue)
    - ``schedule``
    - ``customerCount``
    - ``stock``
    - ``images``
    - ``cancelable``
    - ``stars``
    - ``organizerId`` (reference)
    - ``capacity``
    - ``status`` (draft, published, canceled)
    - ``createdAt``, ``updatedAt``
Business role: Central business object — consumers interact mainly with this. Organizers manage its lifecycle.

### Tickets
- **Description:** Represents tickets owned by customers for a given event.
- **Fields:** 
    - ``id``
    - ``eventId``
    - ``customerId``
    - ``ticketType``
    - ``currency``
    - ``ticketDetail`` (embedded: ticketPrice array[ticketPrices], total double)
    - ``status`` (valid, checked-in, canceled)
    - ``purchaseAt``
Business role: Proof of purchase and access to events. Needed for check-in.
