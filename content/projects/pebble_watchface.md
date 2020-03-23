title: Pebble Watchface
date: 2020-03-22

I have being experimenting with creating a pebble watchface. And I finally made one. I have put almost everything I have learnt so far into the one watchface, which does happen to make it a little complicated.

> Pebble appstore is no longer available so you will need to build from source

So far the things I have added to this watchface are as follows:

* The time (obviously), displayed in either 24h or 12h time.
* The current date and day of the week.
* The battery level of the watch.
* Whether the bluetooth is connected or not.
* Your current steps that you have taken.
* How many steps you should have taken at this point in the day.
* The percentage of your current steps vs your average for either a week day or the weekend.
* And some dials that represent the above data as graphs.

## Notes on the elements

### Battery

The watch only represents the battery meter in tenths, and for some reason I always get that value rounded down to the lowest value. So if your battery is actually at 28% the face will show 20%.

The display will also show if the watch is charging or not. Next to the percentage a `+` icon will display if the watch is charging.

### Bluetooth

The entire background of the app shows the status. If the background is clear (or white) then the bluetooth appears to be connected. If however the background is red then the bluetooth has disconnected. The watch will also vibrate twice when it finds out that the bluetooth has disconnected.

### Time/Date

The time is shown with the hours at the top and the minutes at the bottom. It should also change depending on if you have your watch set to 24 hour or 12 hour display.

The date will show the current day and month in a larger font, with the day of the week shown in smaller text below the date.

There are also two rings that show the time. The blue ring shows the hour as a percentage of the day. So for example if it it 8 o' clock in the morning the ring will be one third full. Where as if it is midday the ring will be half way full. This would be the same as an analog clock if the clock had 24 stops instead of 12.

Then there is the thick pink ring which shows the minutes. This is a percentage of the minutes in the hour (the same as an analog clock).

### Steps count

Your current amount of steps that you have taken today is the larger number in the bottom left corner of the display. The number directly above it is the number of steps you should have taken at this point in the day based on your average activity level.

The percentage on the bottom right of the display is the percentage of the total average steps for the day. And the number directly above it is the average steps that you normally take in the day. The average steps takes into account whether this is a weekend or a week day.

The dial in the very centre of the watch (the purple one) is a representation of the bottom left two numbers on the watch. If the two numbers are almost the same then the ring will be very small and near the top. This means that you are almost perfectly on average of a normal day. If however the ring is filling up to the left that means that you are behind in your steps (you will notice that your current step count is below the average). If however the ring is filling up to the right then you are above your average steps (you will notice that your current step count is above the average).

The ring on the far outside edge (the thin one) is how far your current step count is vs your daily average.

The little piece that moves along this ring is where you should be at this point in the day.

## Planned features for the future

THese are the plans I have for the future, I am unsure when I will do them though.

1. Day/Night theme that changes on sunrise and sunset.
2. Displaying GPS co-ordinates (this is only a possiblity, I will get the information in the above step, but I might not show it).
3. Weather. (I have no need for this to be displayed, but it might be nice to have.)
4. I might add a configuration interface. But this seems unlikely as I can just edit the code when I want to change something.
5. Smoother updates, and making the running time less. Which would in turn use less battery.
