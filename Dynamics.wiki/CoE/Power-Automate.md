# Power Automate – example development practice

> **Scope:** This is general Power Automate development practice. It is deliberately independent of customer, project and solution. Project-specific rules (environments, solution names, prefixes) belong elsewhere, for example in the project's instructions.

These guidelines describe shared development practice for Power Automate flows. Flows should be easy to understand, easy to troubleshoot and maintain, safe to move between environments, and consistent across solutions and developers.

## 1. Flow names

The name describes **what** the flow does, not how it is implemented. Customer and project names do not normally belong in the name.

* Good: `Send Sales Order to ERP`
* Bad: `ACME – HTTP POST v2`

## 2. Description

Every flow has a description in plain language that explains the **business purpose**: why the flow exists and what its most important result or side effect is. Do not just repeat the name or what triggers the flow.

Example: *Creates the required Sales Order records and sends the order to ERP for processing.*

## 3. Action names

Give actions their own names using the pattern `Action | Goal`, so the main flow can be understood without opening each action.

`Compose | Site Address` · `List rows | Annotations` · `Apply to each | Annotations`

## 4. Notes

Use notes (the action description) only where they add value: business rules, non-obvious conditions, workarounds, behaviour in external systems and platform limitations. Do not repeat the action name.

* Good: `ERP requires '/' between each segment of the relative path.`
* Unnecessary: `Creates Site Address` on an action named `Compose | Site Address`

## 5. Expressions

Expressions must be readable. Format long expressions over several lines, and split them into several Compose actions when that makes the logic easier to follow.

```
concat(
    '/',
    items('Apply_to_each_|_Documents')['folder'],
    '/',
    item()['filename']
)
```

## 6. Data retrieval

* `List rows` returns one page of at most 5,000 rows unless pagination is turned on. Turn on pagination (maximum threshold 100,000), or filter so the result is guaranteed to be small.
* The pagination setting does not work with FetchXML queries. For FetchXML, page explicitly.
* Filter in the query itself, not in a Condition afterwards, and retrieve only the columns you need.
* Use `Filter array` or `Select` instead of a loop when you only need to filter or reshape data.

## 7. Error handling

* Put the main logic in a Scope, and handle failures in a separate Scope with Run after set to *has failed*.
* The error message says which action failed and why, not just "Something went wrong".
* Records that fail must be visible (logged or flagged), not silently skipped.

## 8. Environment-specific configuration

Use environment variables and connection references. Do not hardcode URLs, IDs or connections.

## Checklist before a flow is considered done

* The flow has a meaningful name and a description (§1–2)
* Actions have meaningful names (§3)
* Complex logic is documented in a note (§4)
* Long expressions are readable (§5)
* Data is filtered as early as possible and unnecessary loops are removed (§6)
* `List rows` has pagination or a guaranteed small result (§6)
* Errors are handled in a separate scope and failed records are visible (§7)
* No environment-specific values are hardcoded (§8)