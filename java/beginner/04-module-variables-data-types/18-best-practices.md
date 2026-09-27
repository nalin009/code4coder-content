## 18. Best Practices (5+ YOE Expectation)

---

**1.** **Use primitives by default**: Only use wrappers when necessary (collections, null values).

**2.** **Avoid autoboxing in loops**: Cache wrapper objects or use primitives.

**3.** **Always use `.equals()` for wrappers**: Never use `==` for value comparison.

**4.** **Null-check before unboxing**: Prevent `NullPointerException`.

**5.** **Use `Math.*Exact()` for overflow safety**: Especially in financial or critical calculations.

**6.** **Use `final` for constants**: Improves readability and prevents accidental modification.

**7.** **Prefer `valueOf()` over constructors**: Leverages caching for better performance.

**8.** **Use `BigDecimal` for financial calculations**: Never use `float` or `double` for money.

**9.** **Understand caching behavior**: Know the cached ranges to avoid subtle bugs with `==`.

**10.** **Use `var` judiciously**: Only when the type is obvious from context.