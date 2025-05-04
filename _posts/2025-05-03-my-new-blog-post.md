# Amazon E-Book Sales Performance Analysis: Kindle Unlimited vs. Unrestricted Access

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

For books on KU, I pulled the top 5 titles and their respective genres. Then I plotted these with their outright-buy price:

![top-5-titles-on-KU-by-genre-price](https://github.com/user-attachments/assets/c3fe3f9f-7192-427f-b1ca-63871dd526ed)

I found that the best-selling genres on KU tend to be pretty diverse, meaning writing in different genres on KU could be flexible in terms of performance. These books are also priced low to buy outright, with 4 of the top 5 books priced at $1. This could be a **sales strategy** to attract non-KU customers to buy the book for a low price (which is close enough to "free.")

But which genres are most frequently "best-sellers" on KU? (After all, authors get paid for engagement on KU books. Which books have the highest relative metrics of engagement?)

### Genres vs. Best Sellers on KU

Here I plotted the 10 most frequently occurring genres on KU:

![top-10-highest-count-genres-KU](https://github.com/user-attachments/assets/c965d4a4-bf3a-4fcd-a375-4a9cbdfe4f9c)

And here I plotted the 10 most frequent best sellers by genre on KU:

![top-10-genres-best-sellers-KU](https://github.com/user-attachments/assets/bb2eeea4-f141-4e27-99df-8fe7ac865866)

From this, it appears that certain genres have their niches of varying popularity. Among these, some genres are produced more often than others (such as Literature & Fiction, Teen & Young Adult, or Mystery/Thriller/Suspense.)

In other words, you could take 1 of **2 approaches:** write in a popular category and compete with many other books, or write in a niche category and take your chances as a best seller among a smaller audience.

As an example, if you wanted to **write a book in a popular category** such as Mystery and publish it on KU, around 96/3077 (or 0.03%) of similar books are best sellers. Concurrently, if you wanted to **write in a less popular niche** such as a Science/Math book and publish it on KU, you'd have about an 89/385 or a 0.23% chance of writing a best seller.

Therefore, not all niches are equal opportunity; if you wanted to write a Romance book and publish it on KU, you'd contend with 26/1650 or about an average 0.01% chance of writing a best seller. There are many books of this genre in the dataset, but proportionally fewer of them are best sellers even within their own niche.

### So which genre gives you the best odds of success?

Here is a comparison of best sellers in each genre versus the total count of books in that genre on KU among the top 10 genres:

![book-count-vs-best-sellers-in-genre](https://github.com/user-attachments/assets/6511e145-096b-466b-b954-4d00a1eb2b49)

Running some numbers on this, based on the data in the dataset, I found that the "best" and "worst" genres to write in in terms of odds of writing a best seller are: Science & Math (best odds at 0.23%) and LGBTQ+ (worst odds at 0.00%.)

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



