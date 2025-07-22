# my-portfolio
# Building My Interactive Portfolio: A Step-by-Step Journey

I'm excited to share the journey of building and enhancing my personal portfolio website! This project was a great opportunity to apply my skills in front-end development, work with Firebase, and add some modern, interactive features. Here’s a breakdown of what I built and the problems I solved along the way.

### 1. The Foundation: A Modern, Single-Page Portfolio

The website is a single-page application built with **HTML, Tailwind CSS, and vanilla JavaScript**. The goal was to create a clean, professional, and narrative-driven site that tells my career story, highlighting my pivot from a Technical Analyst to an AI Innovator.

### 2. Fixing the "Download Resume" Button & Firebase Integration

One of the first challenges was making sure potential employers could easily download my resume. Initially, the button was not working correctly.

**The Problem:** The "Download Resume" link was inactive. This was a two-part issue: the button's styling didn't clearly indicate it was clickable, and more importantly, the download from Firebase Storage was being blocked.

**The Solution:**

* **Firebase Storage Rules:** The core issue was that the default Firebase Storage security rules were preventing public access to the resume file. I updated the rules in my Firebase project to allow read access to the `saikrishna_resume.pdf` file. This is a critical step for any web app that needs to serve files to users.

    *Rule added in Firebase:*
    ```
    service firebase.storage {
      match /b/{bucket}/o {
        match /saikrishna_resume.pdf {
          allow read;
        }
      }
    }
    ```

* **Robust JavaScript:** I improved the JavaScript code to handle both success and failure when fetching the download URL. If the file is found, the button becomes a prominent blue color. If there's an error (like a permissions issue), the button now becomes disabled and displays "Resume Unavailable," providing clear feedback.

    *JavaScript Snippet:*
    ```javascript
    getDownloadURL(resumeRef)
        .then((url) => {
            // Success: Apply active styles and set the download link
            navResumeLink.href = url;
            navResumeLink.classList.add('text-blue-600', 'hover:bg-blue-100');
        })
        .catch((error) => {
            // Error: Disable the button and show an informative message
            navResumeLink.textContent = 'Resume Unavailable';
            navResumeLink.style.cursor = 'not-allowed';
            console.error("Firebase Storage Error: Could not get resume download URL.", error);
        });
    ```

### 3. Adding an Interactive Mouse Trail

To make the site more engaging, I added a stylish mouse trail effect that follows the user's cursor.

**The Implementation:**

This was achieved with a combination of CSS and JavaScript. A small, blue, circular `div` is created every time the mouse moves. CSS transitions are used to animate its fade-out and shrink effect, and `requestAnimationFrame` ensures the animation is smooth and performant.

* **CSS for the Trail:**
    ```css
    .trail {
        position: fixed;
        height: 8px;
        width: 8px;
        border-radius: 50%;
        background-color: #3b82f6; /* blue-500 */
        pointer-events: none;
        z-index: 9999;
        transform: translate(-50%, -50%);
        transition: opacity 0.6s ease-out, transform 0.6s ease-out;
    }
    ```

* **JavaScript Logic:**
    ```javascript
    document.addEventListener('mousemove', (e) => {
        window.requestAnimationFrame(() => {
            const trail = document.createElement('div');
            trail.className = 'trail';
            document.body.appendChild(trail);
            trail.style.left = `${e.clientX}px`;
            trail.style.top = `${e.clientY}px`;

            setTimeout(() => {
                trail.style.opacity = '0';
                trail.style.transform = 'translate(-50%, -50%) scale(0.5)';
            }, 10);

            setTimeout(() => {
                trail.remove();
            }, 700);
        });
    });
    ```

### 4. Final Touches: Profile Photo & Footer Cleanup

* **Profile Photo:** The final version of the site now correctly loads my professional headshot directly from the project files, ensuring it always displays correctly.
* **Footer Removal:** To create a cleaner, more focused design, I removed the footer section from the bottom of the page.

This project was a fantastic learning experience, combining design, development, and problem-solving. Feel free to check out the live site and let me know what you think!

#Portfolio #WebDevelopment #JavaScript #Firebase #TailwindCSS #AI #Tech

