# A Welcome to Visual Analytics

Today, this blog will transition from solely focusing on statistical analysis with R to further explorations in visual analytics.

**Visual Analytics** is an important part of data science that comes into play after we have done our initial number crunching. It employs creativity and technical skills to put data insights to good use. After all, what is the point of analyzing data if not to find out and communicate something valuable?

Following certain design principles, *good* visual analytics can represent data insights in a quick, concise, and easily understood way. Some of the most common visual representations of data come in the form of images like line graphs, bar charts, or pie charts. These can be helpful in communicating often complex information in a simple, non-technical way.

### *According to Keim et al. (2008), the aim of visual analytics should be to:*
> • Synthesize information and derive insight from massive, dynamic, ambiguous, and often conflicting data. <br />
> • Detect the expected and discover the unexpected. <br />
> • Provide timely, defensible, and understandable assessments. <br />
> • Communicate assessment effectively for action. <br />

## The first given task is to evaluate a data visualization that caught my eye recently.
With the arrival of the recent new year, people tend to like to reflecting back on what happened in the previous one. While finding myself ~doomscrolling~ browsing reflections from 2024, I came across a visualization depicting **which U.S. states saw the most move-in's versus move-out's last year.** Being a ~broke Zillennial seeking to rent a repurposed shipping container under $2,000/mo~ young, aspiring data scientist living in a large city, this finding from the Tax Foundation was particularly interesting to me:

![state-population-changes-attributable-to-interstate-migration-fy-2024-](https://github.com/user-attachments/assets/e9262e51-5833-4c8a-bab8-5b3e1e4402f9)
*(Source: https://taxfoundation.org/data/all/state/americans-moving-to-states/)*

Just glancing at this map without much further interpretation, you can tell that in 2024, many people moved *out* of states like California, New York, Illinois, and Louisiana, among others. At the same time, many people moved *in* to states like Idaho, the Carolinas, and Tennessee, among others.

The Tax Foundation attributes a large part of the incentive for this interstate migration to Americans seeking destination states with lower tax rates. It is also reasonable to surmise that many of these 2024 movers were leaving major cities and flocking to areas with an overall lower cost of living.

### Two other observations that surprised me about this data have to do with my own state and one I've been eye-balling.

Having lived in my metropolitan Florida city for over 16 years now, I have certainly seen exponential population growth, particularly in recent years. Yet according to the map, Florida overall has only seen growth that is slightly above average compared to other states.

While this may be true, it also points to other insights lurking in the data. For one thing, this map depicts *overall* growth as a state, and its purpose is not to show growth differences clustered in certain areas *within* states. It is likely that some cities or counties have growth significantly greater than others within the same state, which can affect one's way of life regardless of overall population growth.

Further, the metric of "1%" can differ drastically depending on the total number of people within the population we're talking about. So while this map offers a good, useful approximation of migratory patterns between states, it does not offer specific details about how many hundreds of thousands to millions of people it represents. Take Wyoming for example - it is widely known that despite the state's size, only about 500 to 600 thousand people live there. According to the data, Wyoming saw a 0.15% rate of population growth in 2024, which to a small population is a much bigger deal.

The other state that caught my eye in this data is North Carolina. Its neighboring states Tennessee and South Carolina do also show significant population growth, indicating that there are lots of people moving to this southeastern region of the country. But I myself had previously considered relocating to NC - and it looks like I'm not the only one who has had that idea! (What can I say? I would miss the food in Florida, but NC has beautiful mountains *and* beaches!)

## How well does this visualization hold up?
In terms of Keim et al.'s standards for visual analytics, this map quickly and effectively communicates the intended information. It makes use of contrasting colors to depict the overall state averages for population growth, such that anyone can quickly glance at the map and interpret the information. It provides both expected and unexpected insights and communicates them effectively.

It does not, however, offer specific details of which cities or areas within these states are seeing the greatest or least population booms. This additional insight might be important for someone who is looking at this map to evaluate their options of where to move. Given that the Tax Foundation identified tax rates as a notable incentive for migratory patterns, it might also be helpful to include individual state tax rates in a similar visualization.

Overall, this goes to show that it is important to decide what question you are asking before you create a data visualization so you can answer it concisely and in a way that is meaningful. Some circumstances might call for an overall approximation, while others might warrant additional details to make informed decisions.
