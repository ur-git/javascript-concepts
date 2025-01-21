# **Event Delegation with Smooth Scrolling Navigation**

## **What is Event Delegation?**
Event delegation is a technique where you attach a single event listener to a common parent element rather than adding listeners to individual child elements. By leveraging **event bubbling**, where events propagate from a child element to its ancestors, you can handle events on dynamically generated or multiple child elements efficiently.

---

## **Steps to Implement Event Delegation:**

1. **Add an Event Listener to a Common Parent Element**
   Attach the event listener to a parent container of the target elements (in this case, navigation links).

2. **Determine the Target Element**
   Use the `event.target` property to identify the specific child element that triggered the event.

3. **Apply Matching Logic**
   Verify that the event originated from the intended child element (e.g., a link with the class `nav__link`).

4. **Perform Desired Actions**
   Execute the event logic, such as preventing the default behavior and implementing smooth scrolling.

---

## **Code Implementation**

```javascript
// 1. Add an event listener to the common parent element
document.querySelector('.nav__links').addEventListener('click', function (e) {
  // 2. Determine if the event target is a link
  if (e.target.classList.contains('nav__link')) {
    // 3. Prevent default behavior of anchor links
    e.preventDefault();

    // 4. Get the target section's ID from the href attribute
    const id = e.target.getAttribute('href');

    // 5. Scroll to the section smoothly
    document.querySelector(id).scrollIntoView({
      behavior: 'smooth',
    });
  }
});
```

---

## **How It Works:**
1. The event listener is added to the parent container `.nav__links`.
2. When a link (`.nav__link`) is clicked, the event bubbles up to `.nav__links`.
3. The `event.target` property identifies the specific element where the click originated.
4. If the clicked element matches the class `.nav__link`, the following occurs:
   - `preventDefault()` prevents the browser's default scrolling behavior.
   - The `href` attribute of the clicked link is extracted.
   - The `scrollIntoView()` method is used to scroll smoothly to the target section.

---

## **Why Event Delegation is Better?**
1. **Efficiency**: Instead of attaching multiple event listeners to each link, one listener handles all links.
2. **Dynamic Content**: Event delegation can handle events for dynamically created elements that don’t exist at runtime.
3. **Cleaner Code**: Centralizes event handling logic in one place, making code easier to read and maintain.