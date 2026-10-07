# Guest Checkout Agent Practice for Rise 360

A self-contained, responsive HTML training component for customer-care agents. It presents random guest checkout questions, lets the learner type a response, and gives immediate rule-based feedback after each answer.

## What the learner does

1. Reads the scenario context.
2. Reads the customer's question.
3. Types a response in the response box.
4. Sends the response.
5. Reviews what was correct, what was missing, and the recommended approach.
6. Moves to the next random customer question.

The simulator uses a shuffled question bag, so the eight scenarios appear in a different order after each restart. Each scenario appears once before the set is reshuffled.

## Included scenarios

| Scenario | Agent should practise |
| --- | --- |
| Guest order missing from My Orders | Explain guest checkout and guide the customer to the relevant magic link |
| Existing account plus guest Apple Pay order | Explain that the guest order is separate from the existing account |
| Several Apple Pay guest purchases | Match the correct order using order number, item, date, and confirmation email |
| Expired magic link | Explain regeneration or route the customer to Care |
| Wrong email | Follow the approved ownership verification process before changing or resending access |
| Customer denies placing the order | Protect order information and follow the fraud escalation process |
| Return or warranty as a guest | Explain how to access supported after-sales help from the guest order page |
| Customer cannot identify the email | Set a privacy boundary and help identify the order safely |

## Files

- `index.html`: Complete component, including HTML, CSS, JavaScript, scenarios, randomization, feedback, and author controls.
- `README.md`: Setup and Rise 360 instructions.

## Rise 360 setup

Host `index.html` on an HTTPS-accessible static host. GitHub Pages is suitable for this component.

If the repository is `aitormaa/Support-Conversation-Simulator`, the expected GitHub Pages URL is:

```text
https://aitormaa.github.io/Support-Conversation-Simulator/
```

In Rise 360, add a Multimedia Embed block and paste this iframe code:

```html
<iframe
  src="https://aitormaa.github.io/Support-Conversation-Simulator/"
  title="Guest Checkout Agent Practice"
  width="100%"
  height="1250"
  style="border:0; display:block;"
  allow="clipboard-write">
</iframe>
```

Use the direct URL only if Rise is configured to embed the page as an iframe. If Rise displays a link preview or metadata card, paste the complete iframe code instead.

## Author mode

Learners see learner mode by default. To show the author controls, add this parameter to the URL:

```text
https://aitormaa.github.io/Support-Conversation-Simulator/?mode=author
```

Author mode includes:

- Scenario selector
- Scenario command
- Customer command
- Model response command
- Apply author scenario
- Copy scenario URL

Example author commands:

```text
/scenario id=severalApplePayPurchases
/customer I bought several times with Apple Pay. Which link should I use?
/reply Identify the correct order using the order number, item, or purchase date, then use the matching confirmation email.
```

## Opening a specific scenario in Rise

Each scenario can be opened directly with a URL parameter. This makes it possible to use one component in multiple Rise lessons:

```text
https://aitormaa.github.io/Support-Conversation-Simulator/?scenario=severalApplePayPurchases
```

Available scenario IDs:

```text
missingFromMyOrders
existingAccountGuestOrder
severalApplePayPurchases
expiredMagicLink
wrongEmail
fraudConcern
returnsAndWarranty
whichEmail
```

Example iframe for a specific lesson:

```html
<iframe
  src="https://aitormaa.github.io/Support-Conversation-Simulator/?scenario=wrongEmail"
  title="Guest Checkout: Wrong Email Practice"
  width="100%"
  height="1250"
  style="border:0; display:block;">
</iframe>
```

## Feedback logic

The feedback is deterministic and client-side. It checks whether the response includes the key behaviors expected for the scenario, including:

- Identifying guest checkout
- Explaining account separation
- Using the correct magic link or confirmation email
- Asking for approved verification details
- Protecting customer information
- Routing fraud or access issues to Care
- Giving a clear next step
- Using a supportive tone

This is intentionally transparent and editable. The feedback is not AI-generated and should be reviewed by the training owner before production use.

## Customizing scenarios

All scenario content is in the `SCENARIOS` array inside `index.html`. Each scenario contains:

- `id`
- `tag`
- `difficulty`
- Context fields
- Customer `question`
- Trainer `note`
- Recommended `model` response
- `criteria` used by the feedback rubric

To add a ninth scenario, add another object to that array. Include at least three criteria so the feedback remains meaningful.

## Limitations

- The component is client-side only.
- Learner responses are not stored.
- Progress resets when the page is reloaded.
- It does not send completion or score data to Rise or an LMS.
- The rubric uses keyword and phrase matching, so a response can be correct even if it receives partial feedback. Review and tune the criteria for your final training content.
- The hosting page must remain available and must allow iframe embedding.
