# Bug Report

## Summary
The **SpeedX Bike Palace** web application contains several bugs that affect functionality, especially in authentication, UI interactions, and data handling.

## Identified Bugs

1. **Incorrect Arrow Function Syntax**
   - File: `index.html` (line ~855)
   - Code: `registeredUsers.find(u => u.username === username && u.password === password);`
   - Issue: Uses `=` instead of `=>`, resulting in a syntax error and preventing login.
   - Fix: Replace with `registeredUsers.find(u => u.username === username && u.password === password);`

2. **Missing Quotes on Image Source**
   - File: `index.html` (line ~273)
   - Code: `<img src=pics\WhatsApp Image 2026-01-21 at 10.11.19 AM.jpeg" alt="Yamaha MT15" ...>`
   - Issue: `src` attribute lacks surrounding quotes, causing the image not to load.
   - Fix: Add quotes: `<img src="pics/WhatsApp Image 2026-01-21 at 10.11.19 AM.jpeg" ...>`

3. **Inconsistent Stock Button CSS**
   - File: `style.css`
   - Issue: `.stock-btn.plus` and `.stock-btn.minus` are hidden by default, but the intended admin mode toggles rely on the `admin-mode` class. The CSS selector `body.admin-mode .stock-btn.plus, body.admin-mode .stock-btn.minus` is duplicated, but the first rule still hides the buttons.
   - Fix: Consolidate the rules to ensure admin mode correctly shows both plus and minus buttons.

4. **Potential Duplicate IDs for Modals**
   - Multiple modals (`loginModal`, `registerModal`, etc.) share the same class `modal` with IDs that are toggled via `classList.add('show')`. Ensure each modal has a distinct ID and that the corresponding JavaScript functions reference the correct element.

5. **Cart UI Not Updating After Adding Items**
   - The `addToCart` function updates the cart but does not refresh the button state if the same item is added multiple times, leading to stale "Add to Cart" labels.
   - Fix: Call `updateButtonStates()` after modifying the cart.

6. **Rental Date Validation**
   - The `calculateRentTotal` function sets `diffDays` to `Math.ceil(diffTime / (1000 * 60 * 60 * 24)) + 1`, which adds an extra day unintentionally.
   - Fix: Remove the `+ 1` or adjust the logic to correctly calculate inclusive days.

## Recommendations
- Apply the above fixes.
- Run unit tests (if any) or manually test login, admin features, cart, and rental flows.
- Consider adding linting (ESLint) to catch similar syntax issues in the future.
