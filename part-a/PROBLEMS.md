# IRCTC Problem Discovery — Part A
 ## Summary - Total problems documented: 6 (3 given + 3 self-discovered) 
 - Platform explored: irctc.co.in (live, as of [date]) 
 - Devices used: [Desktop Chrome / Mobile Safari / etc.]

# Problem 1 - Tatkal Booking Crashes at 10:00 AM

## What is Broken

The IRCTC Tatkal booking system becomes extremely slow and completely unresponsive when Tatkal booking opens at 10:00 AM. Users experience page freezes, server errors, session timeouts, CAPTCHA resets, delayed OTP delivery, and failed bookings. The platform provides little to no feedback about whether a booking request is being processed, queued, or has failed.

This creates panic among users because Tatkal tickets are limited and often sell out within minutes. Users repeatedly click buttons or refresh pages, increasing server load and worsening the problem.

## Affected Users

* Daily Tatkal passengers across India.
* Working professionals making emergency travel plans.
* Students returning home during holidays.
* Families booking urgent journeys.
* Users in Tier 2 and Tier 3 cities who rely heavily on rail travel.

Estimated Impact:

* Approximately 20–40 lakh users attempt Tatkal booking during the peak booking window.
* A significant percentage experience delays, failures, or incomplete bookings.

## Frequency

* Occurs daily.
* Most severe between 9:58 AM and 10:05 AM.
* Has been reported consistently for several years.
* More frequent during holidays, festivals, and vacation seasons.

## Current User Flow

1. User opens IRCTC around 9:50 AM and logs into their account.
2. User searches for a train and selects the desired route.
3. User chooses the Tatkal quota and checks seat availability.
4. User fills passenger information and prepares for booking.
5. At 10:00 AM, the user clicks the "Book Now" button.
6. The page freezes and displays a loading spinner with no progress information.
7. The server becomes slow or returns an error such as HTTP 502 or session timeout.
8. User refreshes the page or tries again.
9. User is often logged out and must sign in again.
10. By the time the user returns, Tatkal seats are sold out or waitlisted.
11. User checks bank account or payment history to verify whether any payment was deducted.

## Where Exactly It Breaks

The failure occurs primarily between Steps 5 and 8.

When thousands of users submit booking requests simultaneously at 10:00 AM, the system struggles to process the load. The user receives no indication of queue position, request status, expected waiting time, or booking progress. Because there is no meaningful feedback, users repeatedly refresh or resubmit requests, creating additional load and increasing the likelihood of system failure.

# Problem 2 - Search Filters Do Not Work Reliably

## What is Broken

IRCTC provides filters such as class, quota, availability status, departure time, and train type to help users narrow down search results. However, these filters often behave inconsistently. Filter selections may reset unexpectedly, show incorrect results, or fail to persist when navigating between pages.

As a result, users spend additional time manually reviewing train lists and verifying information.

## Affected Users

* All users searching for trains.
* First-time users unfamiliar with train classes.
* Senior citizens relying on simple filtering.
* Users booking under specific quotas.
* Mobile users who frequently navigate between screens.

Estimated Impact:

* Potentially affects a large portion of the platform's active user base because train search is the first step of every booking journey.

## Frequency

* Occurs intermittently.
* More noticeable during periods of high traffic.
* Estimated to affect approximately 30–40% of search sessions involving multiple filter changes.

## Current User Flow

1. User enters source station, destination station, and travel date.
2. User clicks "Search Trains".
3. A large list of trains appears.
4. User applies filters such as Sleeper Class, Available Seats Only, and Morning Departure.
5. The results page reloads.
6. Some trains displayed do not match the selected filters.
7. User clicks a train to view details.
8. User returns to the search results page.
9. Previously selected filters disappear or reset.
10. User must manually reapply filters.
11. User eventually stops relying on filters and manually scans all train options.

## Where Exactly It Breaks

The issue occurs primarily between Steps 4 and 9.

Filter settings are not consistently preserved when search results refresh or when the user navigates back from train details. In some cases, availability data appears outdated while filter selections remain active, creating mismatches between displayed results and actual train availability. This reduces user trust in the filtering system.


# Problem 3 - Seat Selection Resets Randomly

## What is Broken

During the booking process, users may select a preferred seat or berth, such as a lower berth for elderly passengers. However, after proceeding to the next step, the selected berth is sometimes lost and replaced with an automatic seat assignment.

This creates frustration because users carefully choose seats based on comfort, accessibility, age, or family requirements.

## Affected Users

* Families travelling together.
* Senior citizens requiring lower berths.
* Pregnant passengers.
* Passengers with disabilities.
* Users booking on mobile devices.

Estimated Impact:

* Around 30–40% of bookings involve berth preferences.
* The issue appears more frequently on mobile devices than on desktop systems.

## Frequency

* Occurs intermittently.
* Estimated to affect approximately 15–25% of bookings involving seat selection.
* More commonly reported on mobile devices due to page refreshes and component reloading.

## Current User Flow

1. User searches for a train and selects a preferred class.
2. User proceeds to the seat selection screen.
3. The seat map loads and displays available berths.
4. User selects a specific berth, such as a lower berth.
5. The selected berth is highlighted as chosen.
6. User clicks the "Proceed" button.
7. Passenger details page opens.
8. The selected berth is no longer displayed.
9. The system shows "Auto" allocation or a different berth number.
10. User returns to the previous page to reselect the berth.
11. The originally selected berth may now appear unavailable.
12. User continues with an automatically assigned seat.

## Where Exactly It Breaks

The issue occurs between Steps 4 and 8.

The seat preference selected on the seat map is not consistently transferred to the passenger details stage. In some cases, page re-rendering, session refreshes, or synchronization issues cause the selected berth information to be lost. Mobile devices are more vulnerable because screen transitions frequently trigger interface refreshes that clear locally stored seat-selection data.

# Problem 4 - Refund Tracking and Status Visibility is Confusing

## How I Found It

I explored the ticket cancellation and refund information flow after reviewing the booking and cancellation sections. I attempted to understand how a passenger would track a refund after cancelling a ticket.

## Screenshot or Description

Suggested Screenshot:
assets/screenshots/problem4-refund-tracking.png

Description:
After cancellation, refund information is displayed across multiple screens and menus. There is no dedicated refund tracker showing current status, expected refund amount, refund stage, or estimated completion date.

## What is Broken

Users who cancel tickets cannot easily track the status of their refund. The platform provides limited visibility into where the refund is in the process, when it will be credited, or whether any action is required.

Many users repeatedly check their bank account or booking history because the system lacks a clear refund progress interface.

## Affected Users

* Users cancelling confirmed tickets.
* Users cancelling waitlisted tickets.
* Passengers affected by train cancellations.
* Users requesting refunds after payment failures.

Estimated Impact:
Potentially affects lakhs of passengers every month who cancel or modify bookings.

## Frequency

* Occurs whenever a refund is involved.
* Affects nearly 100% of users seeking refund status information.

## Current User Flow

1. User books a train ticket.
2. User decides to cancel the ticket.
3. Cancellation request is submitted successfully.
4. User receives a cancellation confirmation.
5. User wants to know refund status.
6. User navigates through booking history.
7. User looks for refund progress information.
8. User sees limited or unclear status information.
9. User checks bank account repeatedly.
10. User contacts support or searches online for clarification.

## Where Exactly It Breaks

The breakdown occurs between Steps 5 and 8.

The system confirms that cancellation has occurred but does not provide a transparent refund tracking experience. Users cannot easily determine refund stage, estimated completion date, or whether processing is delayed.

# Problem 5 - Waitlist Confirmation Chances Are Not Clearly Communicated

## How I Found It

While checking train availability across different dates and classes, I noticed that only waitlist numbers are displayed. There is no clear indication of the probability that the ticket will eventually become confirmed.

## Screenshot or Description

Suggested Screenshot:
assets/screenshots/problem5-waitlist.png

Description:
Train results display statuses such as WL 25, WL 48, or RLWL 12. However, users are not shown confirmation probability, historical trends, or booking confidence indicators.

## What is Broken

The platform tells users their current waitlist position but provides no guidance about the likelihood of confirmation. Passengers often make travel decisions without understanding whether their ticket is likely to be confirmed before departure.

Many users leave IRCTC and use third-party websites to estimate confirmation chances.

## Affected Users

* Waitlisted passengers.
* Festival and holiday travelers.
* Long-distance passengers.
* First-time train travelers.

Estimated Impact:
Affects millions of bookings each year because waitlisted tickets are common on popular routes.

## Frequency

* Occurs whenever waitlisted seats are displayed.
* Especially common on busy routes and peak travel periods.

## Current User Flow

1. User searches for a train.
2. User selects travel date.
3. User views available trains.
4. User notices seat status shows WL 35.
5. User clicks train details.
6. User tries to understand confirmation chances.
7. No probability or guidance is displayed.
8. User searches external websites for prediction.
9. User returns and decides whether to book.

## Where Exactly It Breaks

The failure occurs between Steps 6 and 8.

IRCTC provides raw waitlist information but does not help users interpret it. Users are forced to rely on external prediction services to make informed decisions.

# Problem 6 - Poor Mobile Accessibility and Elderly User Experience

## How I Found It

I opened IRCTC on a mobile browser and compared the experience with the desktop version. I also reviewed accessibility-related options for senior citizens and passengers who may have visual or physical limitations.

## Screenshot or Description

Suggested Screenshot:
assets/screenshots/problem6-mobile-accessibility.png

Description:
The mobile interface contains dense information, small text, multiple dropdowns, and closely packed controls. Important actions are difficult to identify quickly on smaller screens.

## What is Broken

The platform is difficult to use for elderly users, visually impaired passengers, and users with limited digital literacy. Important information is crowded into small areas, and there are limited accessibility enhancements available.

Navigation often requires multiple taps and scrolling, increasing cognitive load.

## Affected Users

* Senior citizens.
* Users with vision difficulties.
* First-time internet users.
* Passengers using small-screen devices.
* Rural users with limited digital familiarity.

Estimated Impact:
Potentially affects millions of users, especially older passengers who depend heavily on railway travel.

## Frequency

* Present during almost every mobile interaction.
* More noticeable on smaller screens and slower devices.

## Current User Flow

1. User opens IRCTC on a mobile browser.
2. User searches for trains.
3. Large amounts of information appear on screen.
4. User attempts to identify important booking options.
5. Small text and crowded layouts reduce readability.
6. User scrolls repeatedly to locate controls.
7. User makes mistakes or misses information.
8. Booking process takes longer than expected.

## Where Exactly It Breaks

The primary breakdown occurs between Steps 3 and 6.

The interface prioritizes information density over accessibility. Important actions are not visually prominent, and there are limited accommodations for elderly or visually challenged users, making navigation difficult and error-prone.
