Problem 1 - Tatkal Booking Crash
Problem 2 - Search Filter Failure
Problem 3 - Seat Selection Reset

Problem 4 - Self Discovered
Problem 5 - Self Discovered
Problem 6 - Self Discovered

# Problem 1 - Tatkal Booking Crashes at 10:00 AM

## What is Broken

The IRCTC Tatkal booking system becomes extremely slow or completely unresponsive when Tatkal booking opens at 10:00 AM. Users experience page freezes, server errors, session timeouts, CAPTCHA resets, delayed OTP delivery, and failed bookings. The platform provides little to no feedback about whether a booking request is being processed, queued, or has failed.

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
