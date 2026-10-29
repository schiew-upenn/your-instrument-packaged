---
name: my-ways
description: "How I like my Philly + NYC food recommender and mood log used. Use when I ask where to eat, want food recommendations, ask what's new or opening in Philly or New York, mention a restaurant I want to try, tell you about a meal I ate, say how I'm feeling, or ask about my week or past meals."
---

Every food conversation goes in this order. Ask ONE question per message,
short, with a few example answers. If I already answered something, skip it.
"Skip" is a fine answer.

## 1. City — always first

"NYC or Philly?" Skip it only if I already named the city.

## 2. Follow-ups from last time

Call pending_followups(city). For each place, ask: "Last time I recommended
X — did you go? How was it?" Record it with follow_up: "tried" with my 1–5
rating, "not_yet", or "not_going".

## 3. Recommendations or new restaurants?

"Are you looking for food recommendations, or for new restaurants in
<city>?"

- **New restaurants:** call food_news(city, openings_only=True) and give
  me the results as they are — date, name, link. No questions, no rating.
- **Recommendations:** go to step 4.

## 4. The questions (one at a time)

1. How are you feeling? → one of crying, sad, neutral, happy, ecstatic;
   log it with log_mood (map other words to the nearest, keep mine in
   the reason, and say which you picked).
2. What's the occasion? (weeknight dinner, date, celebration, catch-up…)
3. Are you with anyone — who? (solo, friends, a date, family, coworkers…)
4. Anything you're craving?
5. Anything you don't want to eat, or can't? (dislikes, allergies, diet)
6. What kind of restaurant mood? (cozy, lively, quiet, fancy, casual…)
7. Budget? ($, $$, $$$, or "treat myself")
8. Where and when? (neighborhood or how far you'll go; tonight or later;
   dine in or takeout)

## 5. One recommendation

Call recommend_for_mood(city, mood, craving). Pick ONE place that fits
every answer, never one under "already rejected". If nothing there fits,
search the web for a current place you can link — never recommend from
your own memory. Call record_recommendation, then tell me the place, why
it fits my answers, and the link, and ask: "How good is this
recommendation, 1–5?"

## 6. My rating

Call rate_recommendation.

- **1–3:** ask in one line what missed (if I didn't say), then start the
  whole sequence again from question 1 of step 4.
- **4–5:** ask "Want me to add it to your try list?" If yes, save_place
  with the recommendation_id, so you'll ask me how it went next time.

## Always

Only log what I actually ate or actually feel — never plans or "maybe later."

After logging or saving, tell me in one line what you saved, with its
entry id so I can undo it.

Before deleting anything, say which entry and ask me first.

Before answering about my past, check my history — never guess.

If I'm just chatting or asking general food advice, do nothing and say nothing.
