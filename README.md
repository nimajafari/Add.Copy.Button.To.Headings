# Add.Copy.Button.To.Headings
Add a copy icon to all headings that have IDs automatically

```javascript
function addCopyIconsToHeadings() {
  // Select all headings with IDs
  const headingsWithIds = document.querySelectorAll('h1[id], h2[id], h3[id], h4[id], h5[id], h6[id]');

  headingsWithIds.forEach((heading) => {
    // Create a span element for the copy icon
    const copyIconSpan = document.createElement('span');
    copyIconSpan.innerHTML = '&#128203;'; // Unicode character for the copy icon
    copyIconSpan.style.cursor = 'pointer';
    copyIconSpan.style.marginLeft = '8px'; // Adjust margin as needed

    // Add click event listener to copy the heading's ID to the clipboard and show a toast
    copyIconSpan.addEventListener('click', () => {
      const idToCopy = heading.id;
      const currentPage = window.location.href;
      const modifiedPage = currentPage + '#';
      if (idToCopy) {
        navigator.clipboard.writeText(currentPage + '#' + idToCopy).then(() => {
          showToast('Link copied successfully!');
        }).catch((err) => {
          console.error('Error copying ID to clipboard:', err);
        });
      }
    });

    // Append the copy icon span after the heading
    heading.appendChild(copyIconSpan);
  });

  function showToast(message) {
    // Create a toast element
    const toastElement = document.createElement('div');
    toastElement.innerText = message;
    toastElement.style.position = 'fixed';
    toastElement.style.bottom = '16px';
    toastElement.style.left = '50%';
    toastElement.style.transform = 'translateX(-50%)';
    toastElement.style.backgroundColor = '#4CAF50'; // Green background color
    toastElement.style.color = 'white';
    toastElement.style.padding = '16px';
    toastElement.style.borderRadius = '8px';
    toastElement.style.zIndex = '1000';

    // Append the toast element to the body
    document.body.appendChild(toastElement);

    // Remove the toast after 3 seconds
    setTimeout(() => {
      document.body.removeChild(toastElement);
    }, 3000);
  }
}

// Call the function to add copy icons and toast messages to headings with IDs
addCopyIconsToHeadings();
```
