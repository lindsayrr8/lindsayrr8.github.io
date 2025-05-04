# Amazon E-Book Best Sellers Analysis: Kindle Unlimited vs. Non-KU

In 1994, the world's largest online retailer began as a small online bookstore in a Washington garage. I am of course talking about **Amazon,** which is so often cited in modern discussions surrounding business and e-commerce.

Though Amazon is not primarily known for its book sales anymore, it still maintains significant influence over the book retail market, both in terms of paper books and digital ones. I recently came across this visualization from [passivesecrets.com](https://passivesecrets.com/amazon-book-sales-statistics/) which shows just how much:

<img width="512" alt="passive secrets amazon book sales" src="https://github.com/user-attachments/assets/d6c851c7-01f4-4497-bd27-1df355f281b0" />

There are already numerous discussions about how Amazon's position in the book retail market affects traditional retail methods like brick-and-mortar bookstores. One strength of Amazon's business model that has enticed 71% of consumers to choose purchasing books online is likely the **convenience** factor. It's quick and easy for someone to add a book to their cart from the same place and within the same transaction that they're purchasing other items. *(I myself have purchased paper books from Amazon before.)*

## E-Book Economics?

One thing I *don't* do is purchase **e-books** from Amazon. Several years ago with the rise of **e-readers,** I acquired a used Kindle Paperwhite to try to make more time for reading as a busy, over-encumbered college student. This changed the game for me as I started renting **free e-books** from my local library via my Kindle. 

Amazon's finance department was a few steps ahead of me, however. In 2014, **Kindle Unlimited** was launched, which offered consumers access to thousands of "free" e-books for a small fee of about $12 per month. But why would consumers pay $12 monthly for access to e-books they can get for free at the library?

Amazon had the answer to that. Any e-books offered on Kindle Unlimited were **not allowed to be offered on any other platform** or by any other service. So if you want an e-book that's on Kindle Unlimited, that's the only place you're going to get it without purchasing it outright.

## An Author's Dilemma

Naturally, as this approach has pros and cons for potential readers, it also has its **pros and cons** for authors.

On one hand, publishing e-books is easier than ever, opening doors for new authors to self-publish and get their work in front of more readers. Someone in Amazon's pool of Kindle Unlimited readers who might have otherwise never given your work a chance could be inclined to give it a try for "free." *(Note that **authors do get paid** for engagement with their work on Kindle Unlimited.)*

On the other hand, publishing an e-book on Kindle Unlimited brings about **two restrictions;** One, if a potential reader does *not* have Kindle Unlimited, they might be less likely to purchase an e-book they could otherwise get for "free" using the subscription. And if they don't have access to the e-book, they might also not purchase the paper book, thus excluding certain readers.

Two, if your e-book is published on Kindle Unlimited, you also cannot publish or distribute the e-book on other platforms like Kobo (or other e-readers), local libraries, or through promotional giveaways, further limiting your pool of potential readers and options for marketing your work.

So what is the best course of action?

# Analysis Objective
As a reader, a writer, and an aspiring data analyst, I decided to **investigate Amazon's e-book sales stats.** I wanted to know about trends like what genres are popular among e-books, which books tend to be best sellers, and whether or not these books are significantly represented by those offered via Kindle Unlimited. 

This way an author could make informed decisions about what genre they write in, what kind of performance they might expect on average, and whether or not they might be better off publishing their work on Kindle Unlimited to give them the best results.

To perform this analysis, I've used [this](https://www.kaggle.com/datasets/asaniczka/amazon-kindle-books-dataset-2023-130k-books) free, publicly available dataset on Kindle E-Books from Kaggle.com. I did a little cleaning and performed mild restructuring on the dataset, then pulled some stats on it using `R`.

# Exploratory Analysis
To start, taking a look at the dataset, there are 133,102 observations or "books" represented. Among the books, 31 genres are included. All of these are e-books, and about **27% of all the books are on Kindle Unlimited.** Probing further, I found that interestingly, about **65% of all best-selling books are available on Kindle Unlimited:**

![all-best-sellers-vs-on-KU](https://github.com/user-attachments/assets/f24f38b8-fd3a-483e-a39a-97615b7b8074)

This is telling. From here, I decided to break down some stats within best sellers that *are* on KU versus those that are *not* on KU to gain some insights across different metrics like genre and price range.

## Books on Kindle Unlimited

For books on KU, I found that the best-selling genres on KU tend to be pretty diverse, meaning writing in different genres on KU could be flexible in terms of performance. These books are also priced low to buy outright, with many of the top performing books priced at $1. This could be a **sales strategy** to attract non-KU customers to buy the book for a low price (which is close enough to "free.")

But which genres are most frequently "best-sellers" on KU? (After all, authors get paid for engagement on KU books. Which books have the highest relative metrics of engagement?)

### Genres vs. Best Sellers on KU

Here I plotted the 10 most frequently occurring genres on KU:

![top-10-highest-count-genres-KU](https://github.com/user-attachments/assets/c965d4a4-bf3a-4fcd-a375-4a9cbdfe4f9c)

And here I plotted the 10 most frequent best sellers by genre on KU:

![top-10-genres-best-sellers-KU](https://github.com/user-attachments/assets/bb2eeea4-f141-4e27-99df-8fe7ac865866)

From this, it appears that certain genres have their niches of varying popularity. Among these, some genres are produced more often than others (such as Literature & Fiction, Teen & Young Adult, or Mystery/Thriller/Suspense.)

In other words, you could take 1 of 2 **approaches:** write in a popular category and compete with many other books, or write in a niche category and take your chances as a best seller among a smaller audience.

As an example, if you wanted to **write a book in a popular category** such as Mystery and publish it on KU, around 96/3077 (or 3.1%) of similar books are best sellers. Concurrently, if you wanted to **write in a less popular niche** such as a Science/Math book and publish it on KU, you'd have about an 89/385 or a 23.1% chance of writing a best seller.

Therefore, not all niches are equal opportunity; if you wanted to write a Romance book and publish it on KU, you'd contend with 26/1650 or about an average 1.58% chance of writing a best seller. There are many books of this genre in the dataset, but proportionally fewer of them are best sellers even within their own niche.

### So which genre gives you the best odds of success?

Here is a comparison of best sellers in each genre versus the total count of books in that genre on KU among the top 10 genres:

![book-count-vs-best-sellers-in-genre](https://github.com/user-attachments/assets/6511e145-096b-466b-b954-4d00a1eb2b49)

Running some numbers on this, based on the data in the dataset, I found that the "best" and "worst" genres to write in in terms of odds of writing a best seller are: Science & Math (best odds at 23.1%) and LGBTQ+ (worst odds at 0.3%.)

```R
> # Show results
> best_genre
# A tibble: 1 × 4
  category_name  all_ku_count best_seller_count success_rate
  <chr>                 <int>             <int>        <dbl>
1 Science & Math          385                89        0.231
> worst_genre
# A tibble: 1 × 4
  category_name all_ku_count best_seller_count success_rate
  <chr>                <int>             <int>        <dbl>
1 LGBTQ+ eBooks         3906                14      0.00358
```

Overall, these odds aren't great, but they do help an author to make an informed decision.

## In that case, how do the odds compare to books that are NOT on KU?

Here, there are a few different factors at play. Now that Kindle Unlimited is not a part of purchase considerations, other things like price will certainly matter more. Does that mean genre sales will perform differently? Once again, only 35% of best sellers in the dataset are NOT on Kindle Unlimited, so the window of opportunity is proportionally smaller.

Pulling the stats for the top 5 best selling titles that are not on KU, there is one damning thing they have in common:

```R
> top_5_bestsellers_non_ku

            author stars price             category_name rank ku_status
1     Sharon Eucce     5     0          Business & Money    1 Not on KU
2      Norah Evers     5     0                Nonfiction    2 Not on KU
3 Matthew Mitchell     5     0                Nonfiction    3 Not on KU
4     Terri DeNeui     5     0 Health, Fitness & Dieting    4 Not on KU
5      Scott Osman     5     0          Business & Money    5 Not on KU
```

...they are all **free!**

That checks out (people love free stuff!) But it's not the best news for a starving author. 

In that case, I went to take a look at more of the *non-zero* price distribution for non-KU best sellers:

![price-dist-best-sellers-not-on-KU](https://github.com/user-attachments/assets/a2657a83-bfaf-4b4d-a298-6a5c9d584b54)


Most of these were under $20 with a few outliers, so I limited the graph to show just the majority and break down the distribution of the price under $20. From that, we can see that many of the e-books cluster in price around $15, $10, and $1. Among these, there were about as many in each of those price ranges as are there are in the $0 price range.

Which leads me to my next question... **does this price distribution differ among *all* best sellers?** Remember that customers who do not have a KU subscription can still choose to outright buy Kindle Unlimited books:

![price-dist-all-best-sellers-under-20](https://github.com/user-attachments/assets/66b73fb4-7f79-442c-bb2a-e42eea6b6b67)

It seems the answer is yes. When all books prices are compared (meaning those with Kindle Unlimited status are combined with those which do not have KU,) it is evident that there are **more books with KU status in the price range of $5 and under.** This is likley another indicator that KU books are also offered at a low price to entice customers who do not have a KU subscription to give them a try via purchasing.

## What does it mean?

In this case I don't have data available with this dataset to see what percent of the best sellers are acquired via KU versus by outright purchase when both options are available for an individual book.

However, it is reasonable to assume that some amount of the 65% of books which are KU best sellers are acquired through both KU and without it. In other words, **books on KU which are also available for purchase have the additional advantage of giving potential readers more buying/acquisition options.**

This potential relationship is even more evident when both options are viewed together:

![price-dist-best-both-ku-and-non](https://github.com/user-attachments/assets/f9d39919-9ea5-4421-8078-2a1edc068dbd)

Further, if Amazon has an algorithmic incentive to advertise KU books to current and potential KU subscribers, that may also be another factor that gives Kindle Unlimited books an advantage.

## What are the odds?

So, if you're a non-KU book, you'll be competing with both KU books *and* the $0 not-on-KU books. Combine this with the fact that many non-KU e-books can also be freely accessed via local libraries. The race between KU and non-KU is really starting to tighten.

But let's look more at that. Suppose you are a brave, non-KU e-book. What factors besides price (such as genre) will give you **better odds of becoming a best seller?**

![top-10-non-KU-genres-vs-best-sellers](https://github.com/user-attachments/assets/dce8de7c-ab9b-44ec-a883-5e2894d8fe5c)

Based on these results, the odds of writing a best selling e-book seem even slimmer for non-KU books than those for KU books did, despite the evident differences in category/genre preference.

If we maintain the assumption that we can take one of two approaches to crafting a potential best seller, being writing a book in a popular genre with many best sellers versus writing a book in a niche genre, then we get the following outcomes:

```R
> best_odds
# A tibble: 1 × 4
  category_name     total_books best_sellers success_rate
  <chr>                   <int>        <int>        <dbl>
1 Children's eBooks        4581           93       0.0203
> worst_odds
# A tibble: 1 × 4
  category_name                total_books best_sellers success_rate
  <chr>                              <int>        <int>        <dbl>
1 Engineering & Transportation        5320           28      0.00526
```

Our optimal chance of writing a best seller in the top 10 genres based on the data in this dataset falls into the Children's E-Books category, being 93/4581 or a 2.03% chance of success when compared to the performance of similar books.

Our worst bet of writing a top 10 genre best seller comes in as an Engineering & Transportation genre book, being about 28/5320 or around 0.53%. Yikes. *(Maybe Engineers already have enough reading to do.)*

*(These numbers go down even more in other genres outside the top 10 genres represented in the dataset. However, there is less engagement overall with those categories.)*

## Interpreting These Results
Quantitatively, this shows that based on the given data, you have **higher chances of writing a best selling e-book in certain categories when publishing via Kindle Unlimited rather than without it.** This differs across genres, and odds of writing a best seller across all genres remain mostly slim.

For better or for worse, when considering the best course of action for a new or non-established author, in most cases **it is worth considering publishing your work via Kindle Unlimited.** This could allow it to reach more potential readers, give those potential readers more buying/acquisition options, and potentially help to corner your specific market based on the genre you're writing in.

However, the **trade off for doing so would exclude you from publishing your work on other platforms** or benefitting from the exposure of sharing your books with local libraries. Based on the findings from the data, I would absolutely recommend prospective authors to do their research in their genre of choice before publishing *(and probably before writing, too.)*

### A few things to note about these findings are that:

A) This dataset does not include revenue for each specific book title. Rather, it groups books by genre into "best sellers" or not. Therefore, the monetary value of an invidiaul "best seller" may be significantly higher from one book to another, which could skew results.

B) This dataset also does not include sales metrics for paper books, many of which can be sold as both a paper book *and* an e-book on Amazon. Therefore, just because an e-book version does not perform well does not necessarily mean that the paper version also sells poorly. This can also skew these results.

C) The dataset also does not specify whether an individual book that is on KU was purchased for the cash price or accessed for "free" via KU, so it cannot evaluate specific sales metrics per book titles in a given genre. What it can do is show an overview of reach to potential readers across genres via the e-book format and/or the Kindle platform.

### Overall success rates according to findings:

```R
 print(success_rates_by_genre, n = nrow(success_rates_by_genre))
# A tibble: 31 × 4
   category_name                sucess_rate_overall ku_sr non_ku_sr
   <chr>                        <chr>               <chr> <chr>    
 1 Arts & Photo graphy          1.5%                7.9%  0.6%     
 2 Biographies & Memoirs        2.5%                7.2%  1.8%     
 3 Business & Money             2.4%                9.6%  1.6%     
 4 Children's eBooks            2.6%                5.1%  2.0%     
 5 Comics                       0.8%                2.8%  0.0%     
 6 Computers & Technology       1.4%                7.4%  0.3%     
 7 Cookbooks, Food & Wine       1.1%                3.1%  0.3%     
 8 Crafts, Hobbies & Home       1.7%                5.5%  0.3%     
 9 Education & Teaching         1.1%                5.4%  0.3%     
10 Engineering & Transportation 1.0%                4.3%  0.5%     
11 Foreign Language             0.6%                1.7%  0.3%     
12 Health, Fitness & Dieting    2.8%                11.6% 1.2%     
13 History                      3.1%                7.8%  1.9%     
14 Humor & Entertainment        0.7%                1.2%  0.3%     
15 LGBTQ+ eBooks                0.3%                0.4%  0.1%     
16 Law                          0.6%                4.5%  0.1%     
17 Literature & Fiction         4.4%                6.9%  1.2%     
18 Medical                      0.5%                6.2%  0.0%     
19 Mystery, Thriller & Suspense 1.7%                3.1%  0.4%     
20 Nonfiction                   5.4%                18.5% 3.2%     
21 Parenting & Relationships    1.2%                3.5%  0.5%     
22 Politics & Social Sciences   2.7%                15.6% 1.8%     
23 Reference                    1.4%                6.4%  0.6%     
24 Religion & Spirituality      2.6%                4.2%  1.7%     
25 Romance                      1.2%                1.6%  0.0%     
26 Science & Math               3.1%                23.1% 1.7%     
27 Science Fiction & Fantasy    0.8%                1.2%  0.1%     
28 Self-Help                    0.8%                2.9%  0.4%     
29 Sports & Outdoors            0.4%                1.4%  0.2%     
30 Teen & Young Adult           2.6%                4.8%  0.9%     
31 Travel                       1.8%                6.2%  0.3%          
```
