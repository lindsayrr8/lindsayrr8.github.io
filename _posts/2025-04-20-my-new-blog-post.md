# Creating a Basic Animation with R

This week, I enjoyed getting to do something that is both new and familiar to me: **creating an animation** with `R`'s `animation` library by Yihui Xie.

One thing I enjoy the most about data analytics and visualization is that it is a very **multi-disciplinary** field. It's a mix of **math, art, and science** *(and maybe a little madness too.)* Therefore, to excel in this field it follows that you'd want to have an aptitude (or at least a tolerance) for all of the above.

Long before I started my journey as an aspiring data analyst, I once attended an art school. Longer before that, I spent the first half of my life creating traditional art. Now I'm both a hobbyist digital artist and a data visualization professional in the works! (Life sure is a whirlwind that way.)

An interest in science was also something that came naturally to me, but an aptitude for mathematics was not. It took me some time and effort to come to the place I'm at today where I grin at the word "statistics" while my brilliant engineering peers cower (muahahaha!)

This blog is not my diary ~~(that's Gemini!)~~ so I won't bore you with the details. But I'd just like to state that the most significant factor in the transformation that led me to the path I'm on today is: **curiosity.**

The thing I love most about data science is the process of figuring things out. I like being able to look at a system where something is happening, riddle it out, and then take action that produces real results based on what I've found.

As such, it gives me immense satisfaction to combine these skills and interests to create...

## A simple data visualization with `animation`

Why do we animate things? For the same reason we visualize things: to communicate information to people.

The cool thing about nature and everything in it is that things are true and at work even if we don't understand them. The purpose of visualization is to either remove ambiguity from something we don't understand on paper, or to transfer something we do understand to others so that we can cooperatively take action that produces results. Sometimes, that visualization comes in a moving form.

The more time I've spent with `R`, the more grateful I am that it is such a simple, concise, and straightforward programming language. It makes tasks like animation extremely simple and approachable.

In the spirit of that, I am sharing my code and the resulting animation with you here so that you can try it yourself if you're also curious:

```R

# Load data and get mean mpg by cylinder
data(mtcars)
agg <- aggregate(mpg ~ cyl, data = mtcars, FUN = mean)
cylinders <- as.character(agg$cyl)
mpg_vals <- agg$mpg

# Animate growing bars
saveGIF({
  for (i in seq(0, 1, length.out = 20)) {
    barplot(mpg_vals * i,
            names.arg = cylinders,
            col = c("skyblue", "orchid", "purple"),
            ylim = c(0, max(mpg_vals)),
            main = sprintf("Average MPG by Cylinder Count (%.0f%%)", i * 100),
            ylab = "Miles Per Gallon")
  }
}, movie.name = "mpg_by_cyl.gif", interval = 0.1)
```

Running the `saveGIF()`function in this case bypasses a few object-hosting headaches like we might have with an `html` object. Instead, we can upload the visualization somewhere as a simple GIF file:

![mpg_by_cyl](https://github.com/user-attachments/assets/281c0c06-077c-4cb3-98db-d3ca64219863)


## Final thoughts
I'm looking forward to making more animated visualizations in the future. I can already imagine the ways I can use this ability to both optimize and express my creativity through my work!
