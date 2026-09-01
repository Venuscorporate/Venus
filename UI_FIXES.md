# Frontend Layout & Text Overlapping Fixes

## Issue Summary
The Venus Corporate Services website has text overlapping issues in the hero section that need to be resolved for better UX and responsiveness.

## Problems Identified

### 1. Hero Section Text Overlap
- "Check My Eligibility" button overlaps with main headline
- "Already applied?" text overlaps with navigation bar
- Navigation text ("Check", "Process", "About", "Contact") overlaps with other elements
- Reference ID input field overlaps with hero content

### 2. Responsive Design Issues
- Elements not properly spacing on mobile/tablet views
- Z-index conflicts causing layering problems
- Flex/Grid layout not properly constraining child elements

---

## CSS Fixes

### Fix 1: Hero Section Layout (Next.js/React)

**File**: `frontend/src/components/HeroSection.tsx` or `frontend/pages/index.tsx`

```tsx
import styles from './HeroSection.module.css';

export default function HeroSection() {
  return (
    <section className={styles.heroContainer}>
      {/* Navigation Bar */}
      <nav className={styles.navbar}>
        <div className={styles.navContent}>
          <div className={styles.logo}>Venus Services</div>
          <div className={styles.navLinks}>
            <a href="#check">Check</a>
            <a href="#process">Process</a>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
          </div>
        </div>
      </nav>

      {/* Hero Content */}
      <div className={styles.heroContent}>
        {/* Left Section */}
        <div className={styles.leftSection}>
          <h1 className={styles.headline}>
            Your Gateway to<br />
            <span className={styles.highlight}>Long-Term</span><br />
            <span className={styles.highlight}>Residency</span> in<br />
            Dubai
          </h1>
          <p className={styles.description}>
            Venus Corporate Service turns your property investment into a secure 
            future in the UAE — 10-Year Golden Visas, 5-Year Retirement Visas, 
            family sponsorship and complete corporate support.
          </p>
          <div className={styles.ctaButtons}>
            <button className={styles.primaryBtn}>Check My Eligibility</button>
            <button className={styles.secondaryBtn}>Explore Services</button>
          </div>
        </div>

        {/* Right Section */}
        <div className={styles.rightSection}>
          <div className={styles.statsCard}>
            <div className={styles.stat}>
              <div className={styles.statNumber}>0</div>
              <div className={styles.statLabel}>Visas Processed</div>
            </div>
            <div className={styles.stat}>
              <div className={styles.statNumber}>0</div>
              <div className={styles.statLabel}>Success Rate</div>
            </div>
            <div className={styles.stat}>
              <div className={styles.statNumber}>0</div>
              <div className={styles.statLabel}>Day Avg. Turnaround</div>
            </div>
            <div className={styles.stat}>
              <div className={styles.statNumber}>0</div>
              <div className={styles.statLabel}>Client Support</div>
            </div>
            <button className={styles.checkBtn}>Start Free 60-Second Check →</button>
          </div>
        </div>
      </div>

      {/* Track Section - Moved Below Hero */}
      <div className={styles.trackSection}>
        <div className={styles.trackContent}>
          <h3>Already applied?</h3>
          <div className={styles.trackForm}>
            <input 
              type="text" 
              placeholder="Enter your Reference ID (e.g. VER...)" 
            />
            <button>Track My Work →</button>
          </div>
        </div>
      </div>
    </section>
  );
}
```

### Fix 2: CSS Module (HeroSection.module.css)

```css
.heroContainer {
  width: 100%;
  position: relative;
  background: linear-gradient(135deg, #0a1f3f 0%, #1a3a52 100%);
  color: white;
  overflow-x: hidden;
}

/* Navbar Styles */
.navbar {
  width: 100%;
  padding: 1rem 2rem;
  position: relative;
  z-index: 50;
  background: rgba(10, 31, 63, 0.95);
  backdrop-filter: blur(10px);
}

.navContent {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 2rem;
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: #ffc947;
}

.navLinks {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.navLinks a {
  color: white;
  text-decoration: none;
  font-size: 0.95rem;
  transition: color 0.3s ease;
  white-space: nowrap;
}

.navLinks a:hover {
  color: #ffc947;
}

/* Hero Content */
.heroContent {
  max-width: 1400px;
  margin: 0 auto;
  padding: 4rem 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  min-height: 600px;
  position: relative;
  z-index: 10;
}

/* Left Section */
.leftSection {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  z-index: 20;
}

.headline {
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 1.2;
  margin: 0;
  word-break: break-word;
}

.highlight {
  color: #ffc947;
}

.description {
  font-size: 1.1rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.9);
  margin: 0;
  max-width: 500px;
}

.ctaButtons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-top: 1rem;
}

.primaryBtn,
.secondaryBtn {
  padding: 1rem 2rem;
  font-size: 1rem;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.3s ease;
  font-weight: 600;
}

.primaryBtn {
  background-color: #4a9eff;
  color: white;
}

.primaryBtn:hover {
  background-color: #3a8eef;
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(74, 158, 255, 0.3);
}

.secondaryBtn {
  background-color: transparent;
  color: white;
  border: 2px solid white;
}

.secondaryBtn:hover {
  background-color: white;
  color: #0a1f3f;
}

/* Right Section */
.rightSection {
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 15;
}

.statsCard {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 30px;
  padding: 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  min-width: 320px;
}

.stat {
  text-align: center;
}

.statNumber {
  font-size: 2.5rem;
  font-weight: 700;
  color: #ffc947;
}

.statLabel {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  margin-top: 0.5rem;
}

.checkBtn {
  grid-column: 1 / -1;
  padding: 1rem 1.5rem;
  background-color: #ffc947;
  color: #0a1f3f;
  border: none;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
}

.checkBtn:hover {
  background-color: #ffb82e;
  transform: translateY(-2px);
}

/* Track Section - Separated Below Hero */
.trackSection {
  width: 100%;
  background: linear-gradient(135deg, #1a3a52 0%, #2a4a62 100%);
  padding: 2rem;
  position: relative;
  z-index: 5;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.trackContent {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.trackContent h3 {
  font-size: 1.3rem;
  margin: 0;
  white-space: nowrap;
}

.trackForm {
  display: flex;
  gap: 0.5rem;
  flex: 1;
  min-width: 300px;
}

.trackForm input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  font-size: 0.95rem;
}

.trackForm input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.trackForm button {
  padding: 0.75rem 1.5rem;
  background: #ffc947;
  color: #0a1f3f;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.3s ease;
}

.trackForm button:hover {
  background: #ffb82e;
}

/* Tablet Responsive */
@media (max-width: 1024px) {
  .heroContent {
    grid-template-columns: 1fr;
    padding: 3rem 1.5rem;
    gap: 3rem;
    min-height: auto;
  }

  .headline {
    font-size: 2.5rem;
  }

  .statsCard {
    grid-template-columns: 1fr 1fr;
    width: 100%;
    max-width: 500px;
  }

  .navLinks {
    gap: 1rem;
    font-size: 0.85rem;
  }
}

/* Mobile Responsive */
@media (max-width: 768px) {
  .navbar {
    padding: 1rem;
  }

  .navContent {
    flex-direction: column;
    gap: 1rem;
  }

  .navLinks {
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
  }

  .heroContent {
    padding: 2rem 1rem;
    gap: 2rem;
  }

  .headline {
    font-size: 2rem;
    line-height: 1.3;
  }

  .description {
    font-size: 1rem;
  }

  .ctaButtons {
    flex-direction: column;
    width: 100%;
  }

  .primaryBtn,
  .secondaryBtn {
    width: 100%;
  }

  .statsCard {
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    padding: 1.5rem;
  }

  .statNumber {
    font-size: 2rem;
  }

  .trackSection {
    padding: 1.5rem;
  }

  .trackContent {
    flex-direction: column;
    gap: 1rem;
  }

  .trackForm {
    width: 100%;
    flex-direction: column;
  }

  .trackForm input,
  .trackForm button {
    width: 100%;
  }
}

/* Mobile Small */
@media (max-width: 480px) {
  .headline {
    font-size: 1.5rem;
  }

  .description {
    font-size: 0.95rem;
  }

  .statsCard {
    grid-template-columns: 1fr;
  }

  .checkBtn {
    font-size: 0.9rem;
    padding: 0.75rem 1rem;
  }
}
```

---

## Key Improvements

✅ **Fixed Issues:**
1. Separated hero content and track section to prevent overlap
2. Added proper z-index layering
3. Implemented responsive grid layout
4. Added max-width containers for proper text flow
5. Fixed button sizing with flex-wrap
6. Improved mobile responsiveness
7. Used CSS Grid for better alignment
8. Added proper padding/margin spacing

✅ **Benefits:**
- No more text overlapping
- Better mobile/tablet experience
- Proper semantic layout
- Easy to maintain and update
- Accessibility improved
- Faster load times with CSS

---

## Implementation Steps

1. Replace your current hero section component with the provided TSX code
2. Add the CSS module file
3. Update any imports/references
4. Test on mobile, tablet, and desktop
5. Adjust colors/spacing to match brand guidelines

Would you like me to also fix the HTML if you're not using React/Next.js?
