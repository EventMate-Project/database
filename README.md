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