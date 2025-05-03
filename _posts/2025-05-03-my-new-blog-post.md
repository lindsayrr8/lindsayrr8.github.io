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

![top-5-on-KU-by-genre-price](https://github.com/user-attachments/assets/5c192104-7e1b-4f85-b65f-2b9b7d92474c)


I found that the best-selling genres on KU tend to be pretty diverse, meaning writing in different genres on KU could be flexible in terms of performance. These books are also priced low to buy outright, with 4 of the top 5 books priced at $1. This could be a **sales strategy** to attract non-KU customers to buy the book for a low price (which is close enough to "free.")


