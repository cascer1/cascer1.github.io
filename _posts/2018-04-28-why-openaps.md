---
title: Why every diabetic should switch to a closed-loop system
tags: [diabetes, OpenAPS, oref0, automation]
categories: [diabetes]
---

On Tuesday October 31st 2017, I flipped the switch (figuratively) to turn on my very own artificial pancreas system.
Since then, I have improved my diabetes care beyond what I ever thought would be possible.
All of this can be attributed to OpenAPS, and the amazing community behind it.

To fully understand this article, you will need a basic understanding of Diabetes (particularly type 1).

Before I begin listing off the many advantages of using a closed-loop system like OpenAPS, I would like to share the story of how and why I started using it.

I’m a member of a community of diabetics from all over the world.
Some of my friends in this community were talking about their systems, and the hard time they were having finding compatible supplies for their rigs.
After hearing their complaints I asked what they were missing; since I had a spare pump lying around and thought maybe it could help someone out.

As it turns out, that pump that had been collecting dust for the last four years was compatible with OpenAPS.
I offered to send it to a friend, but he kindly refused my offer.
At the time he argued that I would need it as a backup pump in case my current one stopped working, but now I know that he refused to take it because he wanted me to use it instead.

Even though I had a compatible pump, I put off setting up my own OpenAPS rig because I thought it required hardware that I did not have.
The documentation at the time was confusing to me, and I was too convinced that it wouldn’t work to even try and figure it out.
This went on for several months.

During the regular visit to my endocrinologist I mentioned to her that some people I know had automated their insulin delivery and adjustments, she responded with a huge smile on her face because one of her other patients had just done the same thing.
While it was impossible for her to officially recommend OpenAPS to me (due to medical regulations), she did very strongly hint that she fully approved the system and would love for me to try it out.

And so I did.

After getting home I immediately contacted my friends that were already using it, asking for help setting everything up.
It turns out that I actually had all the supplies required to set up a basic rig without spending a dime.

The biggest advantage that OpenAPS has to offer in my opinion is its incredible ability to reduce high blood glucose values (BG’s), while simultaneously virtually wiping lows from the table.
Even though it is possible to reduce highs and prevent lows without automation, it takes a lot of work and careful planning; not to mention the huge amount of time you need to invest to monitor your BG, calculate possible adjustments, and then carry out these adjustments.
It’s simply unrealistic to expect any human to react to changes in their BG every five minutes like OpenAPS does.

In addition to always being on top of my BG like I could never be, OpenAPS is much better at calculating and admitting precise corrections.
While I could theoretically achieve the same level of precision, this would require me to carry a calculator; as well as tediously navigating my way through the temporary basal menu every time my sensor gives me a new value.

Another thing OpenAPS does very well is predicting the effect of past treatments before adjusting its insulin dose recommendations.
Where I would simply look at my current BG and go from there, OpenAPS considers how much insulin is still active in my system as well as the trend of my BG (i.e.
is it going up or down? and how much?) before doing anything.
Sometimes, this behavior makes it look like nothing is happening because it is reducing my basal rate even though my BG is too high.
However — looking at the prediction graph — you can see that it expects my values to drop by themselves based on the insulin that is still active in my body.

Even though OpenAPS is designed with security at its core, you can tell it to get on with it and hurry up when you’re done with that high value you’ve been trying to correct for the past two hours.
I can tell it to deviate from my regular target (instead aiming for a lower BG), and administer small boluses (called SMB, or supermicrobolus), to get me plummeting down to reasonable levels.
The first few times you do this, it’s very scary to see how fast it can make your values drop.
However, the system will still operate with the same security considerations it always does.
I have never dropped below the configured target while doing this.
The ability to do this is locked away by default, and should only be enabled after fully understanding the danger of letting your rig give you so much insulin without manual review.
Where the default basal adjustment mode can give me up to 2.4 units per hour, SMB can easily go up to 6 units per hour in my case.

A great advantage of using OpenAPS is its ability to correct very messy situations.
I can go to bed with a too high BG after eating two large servings of pasta, and sleep easy — knowing that I will wake up in-range the next morning.
This was virtually impossible before using OpenAPS because I would either have to sacrifice my sleep (hence, eliminating the ‘sleep easy’ part of my statement) to check and correct my value during the night, or ignore the values and instead wake up feeling bad from the high BG.

Many people are hesitant about using OpenAPS at night — because you are literally trusting your unconscious body to a machine — and I was too when I first started using it.
However, OpenAPS is filled to the brim with safety checks, precautions, and limits, to reduce the risk of giving too much insulin.
The OpenAPS Reference Design explains all the safety considerations that are part of OpenAPS.
By default, the system runs oref0 (OpenAPS Reference Design Zero).
Oref0 can only issue temporary basals below a defined limit.
This limit is defined as the lowest value of:

* The pump's max basal rate
* 3x the maximum daily scheduled basal rate
* 4x the current scheduled basal rate

Furthermore, it will turn off basal delivery after the user has given themselves a bolus and wait for enough data before issuing a new temporary basal command, to avoid interfering with the user input.

If only adjusting temporary basal rates is not enough, it is possible to enable oref1.
Oref1 can deliver boluses, which makes it a very risky but extremely powerful addition to OpenAPS.
Fortunately, oref1 contains several additional safety checks to ensure you never get too much insulin.
It always checks the pump status before and after calculating the required dose to ensure no insulin was given during this time, and sets a temporary basal of 0 for the duration required to offset the just delivered insulin.
So, even if the rig suddenly loses connection to the pump, the user is never in danger of dropping too low.

OpenAPS is completely open-source, and can be found on [GitHub](https://github.com/openaps/oref0).

Now that I have explained how OpenAPS works (and why I think it’s awesome), I’m sure you are interested in actual results — cold hard facts, if you like — from my 6 months of using OpenAPS.

Before I started using OpenAPS, my A1c was 6.8%.
This was the lowest value I had ever reached, and it took a lot of hard work and sacrifice.
I worked out 3–4 times per week, restricted my carb intake drastically (especially for my dinners), and obsessively checked my sensor data.
Even though this result was definitely good, I was exhausted.
I know for a fact that I cannot keep that up forever.

After using OpenAPS for 4 months, I got my A1c tested again.
The result was **6.3%**.
The next two A1c results were both **5.7**.
This might not seem like a drastic improvement, but you haven’t heard what I did to achieve this; I did everything I should not do.
I didn’t go to the gym as much, I stopped eating low-carb, and I had fast food quite regularly.

On top of a reduced A1c, I spent more time in range, and had a more stable line all around.

Using all the methods explained above, OpenAPS can give me what I love most about it: peace of mind.
It doesn’t matter how high my values are, what crazy things I ate just before bed, or that I am suddenly less sensitive to insulin because of a cold.
I never have to worry about my values, because I know that OpenAPS is looking out for me.
always.
