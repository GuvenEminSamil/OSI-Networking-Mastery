# 12-01 — Optional Spaced-Review Guide

> This is an optional resource. It does not create a daily schedule, a required number of study hours, or a mandatory Anki routine.

## 1. Why Review from Memory?

Reading a lesson again can make it feel familiar. But in an exam or a troubleshooting situation, you need to retrieve the information without looking at the page.

Two useful learning methods are:

- **Retrieval practice:** Try to recall an answer before checking the source. Testing yourself can strengthen later recall.
- **Spaced practice:** Review information across separate sessions instead of trying to learn everything in one sitting.

A third useful method is **interleaving**: mixing questions from different topics. For example, alternating subnetting, STP, and DNS questions trains you to recognise which concept applies to a situation.

## 2. An Optional Review Interval

You may use the following intervals as a starting point. They are suggestions, not deadlines:

| Review | Suggested interval |
|---|---|
| First review | 1 day later |
| Second review | 3 days later |
| Third review | 7 days later |
| Fourth review | 14 days later |
| Later review | 30 days later |

Move a card back to an earlier review stage when you cannot explain the answer. Adjust or skip reviews when they do not fit your study pace.

## 3. Choose a Tool Only If It Helps

- **Anki:** An optional flashcard application. You can import the tab-separated text files in `12-REVISION/anki/`.
- **Markdown or paper:** You can keep a small set of questions and answers in a notebook or a Markdown file.
- **Chat-based review:** You can ask for a short quiz on a lesson without maintaining a separate flashcard system.

You do not need to use more than one method.

## 4. Writing Useful Review Cards

1. **One idea per card.** Avoid putting a whole list or an entire OSI model on one card.
2. **Ask why or how.** “Why does a host ARP for the default gateway when sending to a remote network?” is often more useful than “What is ARP?”
3. **Use your own words.** Rewriting an explanation helps you check whether you understand it.
4. **Avoid blind memorisation.** Understand a concept before making a card for it.
5. **Use practical examples.** Change the IP address or topology in a calculation question so that you practise the method, not just one answer.

Example cards:

| Front | Back |
|---|---|
| Why do digital circuits commonly use two logic states? | Two states are comparatively easy to distinguish reliably and work well with transistor switching. |
| What does `0x0800` mean in an Ethernet Type field? | The Ethernet payload contains an IPv4 packet. |
| How does a host decide whether a destination is local? | It compares its own network address with the destination network address using its configured subnet mask. |

## 5. What to Do When You Miss an Answer

| What happened? | Possible reason | Useful next step |
|---|---|---|
| You could not recall it at all. | The idea may not be learned yet. | Revisit the relevant lesson section. |
| You remembered part of it. | Your understanding may be incomplete. | Review the card later and add a concrete example. |
| You were confident but wrong. | You may have a misconception. | Read the lesson's “Common Misunderstandings” section and compare the incorrect and correct ideas. |

## Readiness Check

- [ ] I have chosen a review method that suits me, or decided not to use flashcards.
- [ ] I can explain retrieval practice and spaced review.
- [ ] I can improve a vague or overloaded flashcard by making it more specific.
