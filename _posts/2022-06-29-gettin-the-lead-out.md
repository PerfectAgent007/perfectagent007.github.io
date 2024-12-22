---
title: Gettin' the Lead Out
date: 2022-06-29 14:04:00 -0400
description: Remember when your English teacher told you to save frequently when typing up your essay in the computer lab?...
tags: [Science, Technology]
image: https://i.postimg.cc/vB5F8m2N/manz-cylindrical-cells.jpg
last_modified_at: 2022-06-29 14:04:00 -0400
---

<style>
  .column {width:33%; float: left;}
  p.clear {clear: both;}
  .centerbold {text-align:center;line-height:1.6;}
  li {line-height:1.2}
</style>
<script
  type="text/javascript" id="MathJax-script" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML-full">
</script>

Last month we lost power for five whole seconds. Yup, I'm going full #FirstWorldProblems here. But those five seconds were five seconds too much for a certain battery pack to handle. Uninterruptible Power Supplies or UPS batteries have been mainstream for close to thirty years now, but there's one thing that hasn't changed (that I've seen in the consumer tier) and that's the battery. To the best of my knowledge UPSes have been using Sealed Lead Acid (SLA) batteries for the duration of their product existence, and the UPS for my desktop computer was, until recently, no exception. Why was this a problem for me? Well let's look at the pros and cons of SLA technology.

<div class="column">
  <h4 style="text-align: center">Pros</h4>
  <p>
    <ul>
      <li>Cheap</li>
      <li>Recyclable</li>
      <li>Widespread availability</li>
      <li>an operate and charge below 32°F/0°C</li>
      <li>Sealed construction (no maintenance)</li>
    </ul>
  </p>
</div>
<div class="column">
  <h4 style="text-align: center">Cons</h4>
  <p>
    <ul>
      <li>Heavy</li>
      <li>Environmentally hazardous</li>
      <li>Only rated for 500 charge cycles on average (considerably less when used in a UPS)</li>
      <li>Longevity only maintained if charge doesn’t drop below 50% (2.1v per cell)</li>
      <li>Prone to buildup of internal resistance</li>
    </ul>
  </p><br>
</div>
<div class="column">
  <h4 style="text-align: center">Other</h4>
  <p>
    <ul>
      <li>Battery cells don't require charge management</li>
      <li>Nominal 2.1v per cell yields 12.6v for a 12v battery</li>
    </ul>
  </p>
</div>

<p class="clear">So when the power went out my UPS battery pack was immediately overwhelmed and the unit shut down, along with my computer. By sheer luck I didn’t have anything unsaved, so just the aggravation of having to re-open everything upon bootup is all I had to handle. But of course this was the clearest indication that I needed to replace the batteries in my unit for when I next lost power (spoiler alert: it was about a week and a half later). So just like anyone does that wants to learn more about something, I took to the Internetz.</p>

I’ve read about and seen videos on newer battery technologies in recent years, especially with my interest in home solar power (which is in progress at the time of writing this). But I’ve never really done a deep dive until a few weeks ago. Lithium-ion batteries have been around for decades and are used in tons of portable electronics, power tools, all the way up to electric cars and solar power storage. In general, electrically speaking they can provide the same power output as an SLA and they can withstand more charging cycles, while not suffering too much from going below 50% charge when in use. However Li-ion still ages, and in this particular application it would age very quickly because Li-ion batteries don’t like being at 100% capacity let alone sustained at 100% capacity for long periods of time. This coupled with a rapid discharge when the battery is suddenly providing full power during a power loss, and I don’t imagine the Li-ion battery pack would last very long in my UPS. If I were using the batteries in a frequent charge-discharge application, then Li-ion would work better. And if you’ve seen a bulged Li-ion battery pack before, then that means the battery is chemically compromised and at best will hold very little charge, and at worst could catch fire or explode in the right conditions. I prefer things only go KABOOM when they have my permission to do so. Something else to take into consideration is how close to 12v can Li-ion get when cells are combined in series. For a 12v battery pack you can either go three cells in series or four to get 11.1v or 14.8v respectively when using 3.7v (nominal) cells. For undervolted batteries there will be a higher current draw which results in two things – shortened load times and heat. For overvolted batteries, like with anything, you run the risk of damaging anything connected to it.

<div class="column">
  <h4 style="text-align: center">Pros</h4>
  <p>
    <ul>
      <li>Longer effective battery life</li>
      <li>Can withstand thousands of charge cycles</li>
      <li>Higher charging efficiency than SLA</li>
      <li>Less prone to internal resistance than SLA</li>
      <li>More environmentally friendly</li>
      <li>Higher voltage per cell</li>
      <li>No battery memory</li>
    </ul>
  </p><br>
</div>
<div class="column">
  <h4 style="text-align: center">Cons</h4>
  <p>
    <ul>
      <li>Maintaining 100% charge level shortens lifespan of the battery</li>
      <li>Full discharge shortens the lifespan of the battery</li>
      <li>Like with SLA, supported charge cycles are shortened with deeper charges/discharges</li>
      <li>Possibility of bulged cells long term</li>
      <li>Costs more than SLA</li>
    </ul>
  </p>
</div>
<div class="column">
  <h4 style="text-align: center">Other</h4>
  <p>
    <ul>
      <li>Battery management circuitry required to prevent overcharging</li>
      <li>Nominal 3.7v per cell doesn’t multiply well for common load voltages (e.g. 11.1v (3.7×3) for 12v load or 51.8v (3.7×14) for 48v load)</li>
    </ul>
  </p>
</div>

<p class="clear">Lithium polymer batteries use very similar technology, the main difference between Li-ion and Li-Po being a solid vs liquid/gel electrolyte between the positive and negative electrodes. Li-Po batteries are safer than straight up Li-ion, but they also cost considerably more and aren’t as dense, so you get less capacity for your battery’s form factor. Also the use of a flexible polymer in the battery construction allows for a flexible battery pack. But since none of this is beneficial in the context of a UPS battery replacement, I’ll skip a breakdown of this.</p>

NMC (Lithium Nickel Manganese Cobalt Oxide) and NCA (Lithium Nickel Cobalt Aluminum Oxide) I’m also skipping because not only are they not as readily available as Li-ion or Lithium Iron Phosphate (which I’ll get into in a minute) they need to be cooled. Additionally they’re quite volatile if something goes wrong internally. If you’ve read about Tesla cars catching fire after a battery cell being ruptured due to a collision, this is why.

Nickel Cadmium (NiCad) and Nickel Metal Hydride (NiMH) are very old technology. NiCad is actually banned in a lot of places because of the use of mercury within the cells alone, to say nothing of its much lower capacity and long charge times compared to Li-ion. I had a few of these batteries in RC cars when I was a kid and man did I hate life because of them – four hours of charge time for a lousy twenty minutes of run time and these were the <$50 cars, not the $200 models. NiMH is still in use today, and you typically see them as the big brand rechargeable cells. The main reasons NiMH is still around is they are cheaper than Li-ion but they also generate a nominal voltage of 1.2v per cell compared to Li-ion’s 3.7. Depending on your usage case, a 1.2v cell can be more optimal. Another bonus is that NiMH batteries don’t have transportation restrictions. But instead of an operative word, there’s an operative number here: 1.2. For a 12v battery it will take ten cells just to get the required voltage, never mind pack enough amperage to last a while. So naturally NiMH is out.

<div class="column">
  <h4 style="text-align: center">Pros</h4>
  <p>
    <ul>
      <li>Cheaper than Li-ion</li>
      <li>Somewhat environmentally friendly</li>
      <li>Widely available</li>
    </ul>
  </p>
</div>
<div class="column">
  <h4 style="text-align: center">Cons</h4>
  <p>
    <ul>
      <li>Only 1.2v nominal</li>
      <li>Lowest charge density</li>
      <li>Charges slower than Li-ion</li>
      <li>Cells can experience nominal voltage depletion if not discharged and recharged every few months</li>
    </ul>
  </p><br>
</div>
<div class="column">
  <h4 style="text-align: center">Other</h4>
  <p>
    <ul>
      <li>Would need 50 18650 NiMH cells at 4000mAh in 10s5p configuration to create a 12v 20Ah UPS battery (my original batteries were 12v 18Ah)</li>
    </ul>
  </p>
</div>

<p class="clear">And finally we come to what I decided on purchasing: Lithium Iron Phosphate (LiFePO4 or LFP). LiFePO4 cells have a nominal voltage of 3.2v per cell, so 12.8v in a 12-volt pack, but they pack a bit less charge capacity than Li-ion. An 18650 LiFePO4 cell maxes out around 2000mah while a Li-ion cell of the same size will top out at 3500mah. Multiplying the voltage by the capacity gets us 6.4Wh for a LiFePO4, but 12.95Wh for Li-ion. So why would I go for the lower capacity battery? Well let’s dive a little deeper.</p>

Every battery regardless of chemistry will have a range of usable charge that is smaller than someone might think at first glance. Not many devices will actually give live readouts of the voltage in a battery cell, they will only report a percentage. The 0-100% range is what we’re used to, but this doesn’t actually represent the full 0-100% range of the battery itself. I mentioned before that SLA batteries don’t like to be discharged below 50% or else the lifespan is significantly shortened. This is because at these levels sulfation occurs, which reduces the amount of active materials inside the cell, thereby reducing available power. So with SLA you effectively only get 50% of the battery’s potential. A 12v 12Ah battery pack can give you a theoretical 144Wh of power but once you’ve done that just a single time you’re never going to get it again. Even worse is just the second discharge cycle can be as little as 50% of the original capacity depending on how low the battery was discharged and/or how long until the battery was recharged. Sometimes you don’t even get that second discharge cycle if the battery has been sitting long enough. Like anyone else, I like a battery that can maintain its charge for a decently long period of time.

Li-ion and LiFePO4 maximum and minimum voltages are different than SLA, but they have similar limitations. In the case of lithium batteries you have a battery management system (BMS) with almost every (if not every) battery pack in existence to balance each battery cell so their voltages are near identical (if the BMS has this feature) and to prevent overcharging and overdischarging. A LiFePO4 BMS it is specifically designed to protect and thereby extend the battery’s lifespan as long as possible by preventing a battery from going below 2.5v when discharging, or above 3.65v when charging. But obviously 0% isn’t 0v. The BMS cutoff points of 2.5v and 3.65v are the 0% and 100% points respectively. The BMS is also why lithium-based batteries last so much longer than an SLA equivalent. When you have a manager that can cut off the load before the voltage gets too low, low enough to damage the battery, this lets us have those extra charge/discharge cycles so that we can keep using the battery for years. But hang on a minute, the high and low cutoff points for li-ion are 4.2v and 2.5v, giving us about another .7v of range to play with. Couple that with the higher density per cell and, going by the math, a 12Ah li-ion pack (I’m using 12Ah as an arbitrary number, not the actual amount you’d find in a manufactured 12Ah pack) you’d have somewhere in the vicinity of 50% more usable charge. So why choose LiFePO4 over li-ion? Now is when we have to go beyond the math. If capacity alone was enough for me, I’d have gone with li-ion.

In the real world a 12v li-ion pack is made up of three 3.7v cells. And yes $$3.7 \times 3 ≠ 12$$, but then neither does $$3.7 \times 4$$. So at nominal voltage you get either 11.1v in a 3-cells-in-series pack (referred to as 3s) or 14.8v in a 4s pack. 11.1 is a lot closer to 12 than 14.8, but I can only speculate the reasons the industry chose 3s for li-ion 12v packs since a lot of electronics will run on 14.8v since that’s a common voltage for a lot of laptops.

Since LiFePO4 cells are 3.2v, four of these in series yields 12.8v, which is not only closer to 12v than with li-ion, but also only goes over 12v by a much smaller amount than with a 4s li-ion battery. When you set your load to a constant draw, higher voltage means less current draw, which is a lower strain on the battery cells as well as less heat. But let’s do a little more math:

<div class="column">
  <h4 style="text-align: center">SLA 12v pack in 6s</h4>
      <p class="centerbold"><b>Theoretical:</b></p>
      <p>$$\begin{gather}
          6 \times 2.1v = 12.6v\\
          12.6v \times 12Ah = 151.2Wh
          \end{gather}$$
      </p>
      <p class="centerbold"><b>Real:</b></p>
      <p>$$\begin{gather}
          2.3v-1.75v  =0.55v\\
          \text{(full charge vs dead)}\\\\
          6 \times 0.55v = 3.3v\\
          \text{(usable voltage across all cells)}\\\\
          3.3v \times 12Ah = 39.6Wh ~ \text{usable}
          \end{gather}$$
      </p>
</div>
<div class="column">
  <h4 style="text-align: center">Li-ion 12v pack in 3s</h4>
      <p class="centerbold"><b>Theoretical:</b></p>
      <p>$$\begin{gather}
          3 \times 3.7v = 11.1v\\
          11.1v \times 12Ah = 133.2Wh\\
          \end{gather}$$</p>
      <p class="centerbold"><b>Real:</b></p>
      <p>$$\begin{gather}
          4.2v-2.5v = 1.8v\\
          \text{(range limited by BMS)}\\\\
          3 \times 1.8v = 5.4v\\
          \text{(usable voltage across all cells)}\\\\
          5.4v \times 12Ah = 64.8Wh ~ \text{usable}
          \end{gather}$$
      </p>
</div>
<div class="column">
  <h4 style="text-align: center">LiFePO4 12v pack in 4s</h4>
    <p class="centerbold"><b>Theoretical:</b></p>
      <p>$$\begin{gather}
          4 \times 3.2v = 12.8v\\
          12.8v \times 12Ah = 153.6Wh\\
          \end{gather}$$</p>
      <p class="centerbold"><b>Real:</b></p>
      <p>$$\begin{gather}
          3.65v-2.5v=1.15v\\
          \text{(range limited by BMS)}\\\\
          4 \times 1.15v = 4.6v\\
          \text{(usable voltage across all cells)}\\\\
          4.6v \times 12Ah = 55.2Wh ~ \text{usable}
          \end{gather}$$
      </p>
</div>
<p class="clear"></p>

Looking at the numbers above, li-ion is indeed the clear winner for capacity, though LiFePO4 does come in a decently close second. And as I said before if capacity was my only goal I’d have gone with li-ion packs. But I also care about two more things: overall longevity and heat. LiFePO4 cells are rated for easily ten times as many charge/discharge cycles as li-ion and certainly a hundred times more as SLA. But since SLA and li-ion don’t like staying at 100% charge for prolonged periods of time, just by sitting and waiting for a power load will shorten their life span. LiFePO4 is by no means invulnerable, but then out of all battery chemistries to date it is the most hardened to it. Translating this into potential real-world numbers, an SLA UPS battery might last between 5 and 20 cycles depending on the frequency and duration of power interruptions, a li-ion could go between 10 and 50, but I would expect a LiFePO4 to go between 50 and 200. But most importantly an SLA UPS battery might last a few years at most before it can’t sustain any load even if only discharged two or three times. Li-ions are rated at 8 to 10 (I’ve never actually owned one for a UPS battery so I can’t speak to real-world test results) but I imagine they would definitely last 6 to 8. LiFePO4 are rated for 10 years but I expect that it could push through ten years without breaking a sweat. And because LiFePO4 batteries don’t heat up under load, this combined with the lower current draw due to the higher total voltage output in a 12v battery pack makes them very appealing.

So now my 900W UPS has two 12v 18Ah LiFePO4 packs in it and during the prolonged power outage I decided to test a gaming load since I still had an internet connection. Playing Star Trek Online (the game I happened to be playing when we lost power) I was pulling down about 360W peak, with 90-100W of that being my three monitors. My UPS display fluctuated between 35 and 50 minutes of backup time, which is several times what I’ve been able to get in the past under SLA batteries in the same unit. Maybe next time I feel like doing a test I’ll load up Shadow of the Tomb Raider or Horizon Zero Dawn? “Run time during power loss” would make for an interesting benchmark statistic.

The one thing I didn’t get to do, which I am noticing a lot of people on YouTube doing, is testing the capacity of the battery to see if it’s living up to the rating on the label. My packs are 18Ah each but do they really have that capacity? Unfortunately I don’t have the measuring equipment needed to log all of this, though it’s not hard to get. The question of capacity also brings up one for the future – can a 6v or 12v LiFePO4 UPS battery be DIYed and have more capacity than a manufactured one? Well considering that during the power outage there were seven UPSes that all ran dead I imagine I’ll be needing to replace a number of battery packs so that they can even run the next time we have an outage, rare as they are in my area. I’m definitely going to try doing this in the future so keep an eye out for that post because you can be sure I’m going to share what I learned.