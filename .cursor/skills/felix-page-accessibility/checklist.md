# Designer checks for one page

The standard is WCAG 2.1 Level AA. Apply a line only when that content is on the page. A line with no matching content is skipped, not a failure. A line marked human check is reported, not invented.

## Text alternatives

- Every image that carries meaning has alt text written after looking at the image. (1.1.1)
- A decorative image has empty alt text. (1.1.1)
- Text that matters is real text, not only a picture of words, when the element tree shows the words are an image. A logo may stay an image. (1.4.5)

## Keyboard and structure

- Buttons and links are button, text link, or link block elements, or a control with an explicit role and `tabindex="0"`. (2.1.1, 4.1.2)
- No `tabindex` greater than 0. (2.4.3)
- No link without a destination. (2.4.4)
- No empty link or empty button. An icon has a name. (4.1.2)
- A link name says where it goes. “Read more” and “Click here” are failures when the destination is known. (2.4.4)
- The visible text of a control is the start of its accessible name. (2.5.3)
- A custom widget, such as a calculator, a dropdown, or a tab, exposes its name, role, and state. (4.1.2)
- Headings do not skip a level. (1.3.1, 2.4.6)
- The page has one h1, then h2, then h3. (1.3.1)
- A group of related items is a list element when the structure is already a list. Do not rebuild a layout into a list. (1.3.1)
- Header, navigation, main, and footer are landmark regions when those elements exist on the page. (1.3.1)
- A skip link is present in the shared header. Confirm it. Do not add a second one. (2.4.1)
- Closed or hidden panels are not given a positive tabindex. (2.4.3)
- A passage in a different language from the page has that language set on the element. Do not tag a proper name. (3.1.2)

## Contrast and focus

- Solid text on a solid background is at least 4.5:1. Large text, 18 pt or 14 pt bold, is at least 3:1. (1.4.3)
- Icons and field borders on a solid background are at least 3:1. (1.4.11)
- Text on a photo has a solid background behind it, or is reported as a human check. (1.4.3)
- Color is not the only signal on an error or a selected state that is visible in the Designer. (1.4.1)
- Each link and button class on this page has a visible focus style. `outline: none` with no replacement is a failure. (2.4.7)
- Content that opens on hover or focus can be dismissed and stays open while the pointer is on it. If the Designer cannot show that behavior, it is a human check. (1.4.13)

## Forms

- No field uses autofocus, and focusing a field does not change the page. (3.2.1)
- Changing a field does not submit the form. (3.2.2)
- Every field has a visible text label in the Designer. Placeholder text does not count. (3.3.2)
- A field that collects name, email, or phone has the matching autocomplete token when the setting exists. (1.3.5)
- An error element that already exists is next to its field and says what is wrong. Where the fix is already written, it says how to correct the field. (3.3.1, 3.3.3)
- A missing error state is a human check, not a failure to invent.
- A result that appears without a page load is a status message. If no live region exists, report it as a human check. (4.1.3)
- A form that submits a transfer, a payment, a legal commitment, or a deletion is a human check for review, correction, or confirmation before it is final. (3.3.4)
- A time limit is a human check. Do not build an extension control. (2.2.1)

## Media and motion

- Media that is set to autoplay is a failure when the setting can be turned off. (1.4.2, 2.2.2)
- An iframe has a `title` that names it from the heading or label already on the page. A decorative background iframe is hidden with `aria-hidden="true"` and `tabindex="-1"` instead. (4.1.2)
- A video without a caption track already on the page is a human check. (1.2.2, 1.2.5)
- Flashing, parallax, and scrolljacking cannot be cleared from the element tree. Report them as a human check. The flash limit is 3 flashes in any one second. (2.3.1, 2.2.2)

## Page settings

- The page title is not empty. (2.4.2)
- The locale being edited matches the page language the developer named. Spanish is the default. (3.1.1)
