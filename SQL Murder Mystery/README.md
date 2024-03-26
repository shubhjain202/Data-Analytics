The mystery starts here and provides you with just three pieces of information: the crime was a murder, and it occurred sometime on Jan. 15, 2018, in SQL City.
Here is the database schema diagram.

The first query is to find the crime scene report for a murder on that date and time.
![Alt Text](/SQL%20Murder%20Mystery/Images/q1.png)


This leads us to try to find the two witnesses. We can do that in one query, placing an OR in between the two.


We have a lot of information from gym membership, license plate number, and gym attendance. We're looking for someone who has a membership id starting with 48Z, has a gold membership, worked out on January 9th, and has a license plate H42W. If we're really on top of things, we can answer this question in one query.


Bear with me here. We have get_fit_now_check_in, which tells us the check-in date. Then get_fit_now_member will tell us the membership status. We can use membership_id and id to join those tables together and use WHERE to filter out the check-in date and membership status. (I could have also put in '48Z' as part of the membership ID, but it wasn't necessary.)
Still, to get who the person is in one query, we need to join the person's name and driver's license. We got those from joining name from the get_fit_now_member table to name from the person table. We then join driver's license on the id column. In the WHERE statement, we add the digits of the driver's license, which narrows it down to the murderer.

But wait, there's more! We go back to Jeremy's interview report (why we didn't think of doing that from the outset is another mystery), and he gives us the following information:
I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017.
There's a lot of information to be gleaned from the driver's license, but we'll need to match it up with the person table to get the possible names. (We can use income, too, although "a lot of money" is subjective and doesn't tell us much. I initially included it but found it unhelpful.)

I filtered for a female with red hair who drives a Tesla Model S. Two options came up. Both were between 65 and 67 inches tall (which was a little confusing in the initial question since it says 5'5" or 5'7", not between the two), so I didn't bother going back to include it in the WHERE statement.

(Later in the table, it showed that both were making over $270,000 per year.)
Now, we just need to find which one of these suspects attended the symphony three times in December.

We need to join the person table to facebook_event_checkin to find the person's name. The count will tell us how many times that person attended the event. The WHERE statement gives us a date between 20171201 and 20171231 (thankfully within only one month so I didn't need to deal with datetime logic). The GROUP BY and HAVING statements tell us which people attended the event exactly three times in December 2017.

Boom, we have our answer. It's Miranda Priestly, not Red Korb. She's the one who hired Jeremy Bowers to commit the murder.