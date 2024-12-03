---
title: Concurrency Crises and Buyer-Seller Shenanigans - Why Formal Methods Keep Us Sane
date: 2024-12-03 10:00:00 +0000
categories: arcipilago
tags: [arcipilago, petri-nets, formal-methods, ccs]
excerpt: "The formal methods"
---

---

> My write-up can be subjective. I understand that not everyone will necessarily agree with my points. Please don’t waste your time trying to prove me wrong, but if you see something really wrong, feel free to let me know.
> Please try to use private-mode in your browser while reading this write up as it helps in retrieving the latest contnet of the blog.
> {: .prompt-warning }

---

In my previous post from this series [Science in Software Development](https://dhivakar020.github.io/posts/science-in-software-development/), i had this section called [Asking the right questions](https://dhivakar020.github.io/posts/science-in-software-development/#asking-the-right-questions). One of the main question was "Is there a formulated/scientific way to measure software aspects?". The answer to this question is complicated. While not every software development aspects have a formulated way, there are some particular resources available in internet that can help us to have a formulated/objective way to design applications. One such resource comes from the 9th International School on Formal Methods for the Design of Computer, Communication, and Software Systems. This event is shortly called as SFM 2009.

### The theme of SFM 2009 was,

The event was dedicated to exploring formal methods applicable to web services, covering a variety of topics such as:

- **Choreography and Orchestration**: Techniques for coordinating interactions among services.
- **Description Techniques**: Methods for formally describing service behaviors.
- **Interaction and Composition**: How services interact and can be composed together.
- **Session Types and Contracts**: Formal frameworks for ensuring correct interactions between services.
- **Verification and Security**: Ensuring that services behave as intended and are secure.
- **Performance Analysis**: Evaluating the efficiency of service interactions.

## Why this write-up,

- First of all, i am not going to explain about all the formal methods. Because it's not about making tutorial, it's about sending a message about the significance of formal methods.

![sending a message](/assets/img/formal_methods/sending_a_message.jpg)

- I am going to use formal methods to design three communication systems, and to evaluate them.

## Buyer / seller compatibility,

Note:

- I am using **Petri Nets** to design Models,
- Ports and adapters are given as a square between the two services/modules, Buyer and Seller.
- Processes in the service communicate to the other services through the ports that are same color as the process.
- I am using CCS - Calculi for Communicating systemnote and evaluate communications.

#### Buyer and Seller Process,

$$
B ≙ ord.(prod̄ | inv̄.pay)
$$

This expression describes the buyer’s behavior:

1. **`ord`**: The buyer places an order.
2. After placing the order, the buyer expects two concurrent actions:
   - Receiving the product (`prod`).
   - Receiving an invoice (`inv`) and then making a payment (`pay`).

$$
S ≙ ord̄.inv.paȳ.prod
$$

This expression describes the seller’s behavior:

1. **`ord̄`**: The seller receives an order.
2. **`inv`**: The seller sends an invoice.
3. **`paȳ`**: The seller waits for payment.
4. **`prod`**: The seller delivers the product.

### **Key Steps in the Interaction:**

1. **Order Placement and Receipt:** The buyer places the order (`ord`), and the seller receives it (`ord̅`):
   $$
   B | S → τ → (prod̄ | inv̄.pay) | inv.paȳ.prod
   $$
2. **Invoice and Payment:**

- The seller sends the invoice (`inv`), and the buyer receives it (`inv̅`).
- The buyer sends payment (`pay`), and the seller receives it (`pay̅`):
  $$
  τ → (prod | paȳ) | paȳ.prod
  $$
  $$
  τ → (prod̄ | 0) | prod
  $$

3. **Product Delivery:**

- The seller delivers the product (`prod`), and the buyer receives it (`prod̅`):
  $$
  τ → (0 | 0) | 0
  $$

#### Model - 1 ,

![Model 1](/assets/img/formal_methods/model_1.png)

After introducing recursion,

{::nomarkdown}
$$ S′ ≙ rec X. ord̄.inv.paȳ.prod.X $$
{:/}

- The seller performs the actions `ord` (receive an order), `inv` (send an invoice), `pay` (process payment), and `prod` (deliver the product).
- After completing these actions, the process `X` repeats itself indefinitely.

- **Strengths**:

  - **Sequential execution** ensures that every step (order, invoice, payment, product delivery) must complete before the process goes recursion.
  - This strict ordering minimizes **race conditions** because actions are dependent on the successful completion of the previous step.
  - Easier to audit for **security-business logic flaws** since the workflow is linear and predictable.

- **Weaknesses**:
  - **No concurrency**: If one part of the system fails (e.g., payment service), the whole process stalls.
  - **Not robust to partial failures**: Recovery or retries for individual steps are not naturally supported.

#### Model - 2 ,
