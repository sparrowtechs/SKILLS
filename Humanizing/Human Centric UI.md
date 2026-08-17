# Human Centric UI

## Purpose

Design interfaces that feel **intentional, human, product-specific, premium, and effortless to use** rather than generic, template-driven, or obviously AI-generated.

This skill is not about banning modern design techniques.

The goal is:

> **Make the right design decision for this product, rather than the statistically common design decision an AI would normally make.**

Prioritize:

1. Clarity
2. Usability
3. Product fit
4. Information hierarchy
5. Accessibility
6. Distinctive identity
7. Visual refinement
8. Decoration

Never reverse this order.

## Use This When

Use this skill when:

- designing a new UI, screen, or flow
- redesigning an existing interface
- reviewing UI for clarity, hierarchy, accessibility, product fit, or generic AI-like patterns
- rewriting interface copy to sound more natural and product-specific
- refining hierarchy, visual direction, product fit, or interaction clarity

Do not use this skill for:

- backend architecture
- purely technical debugging
- non-UI implementation work with no product, UX, or copy decisions
- visual tasks that must mechanically follow a locked design system with no room for interpretation

## Modes

### 1. New UI Design

Use when creating a new screen or flow from scratch.

Steps:

1. Identify the user, task, and product context.
2. Define the primary action and information hierarchy.
3. Choose layout, navigation, and interaction patterns.
4. Apply visual restraint and product-specific design choices.
5. Test the screen against edge cases and accessibility needs.
6. Run the anti-slop review and remove unnecessary elements.

### 2. UI Review

Use when evaluating an existing screen, flow, or mockup.

Steps:

1. Identify what the screen is for and what the user should do first.
2. Check clarity, scanning, hierarchy, and action prominence.
3. Review copy for natural language, brevity, and relevance.
4. Review visual language for generic AI tropes, weak product fit, or unnecessary decoration.
5. Check accessibility, responsiveness, and edge-case handling.
6. Summarize the problems, then recommend revisions.

### 3. Copy Refinement

Use when improving interface text without redesigning the whole UI.

Steps:

1. Replace technical or inflated wording with user language.
2. Remove redundant explanation and filler text.
3. Shorten labels, descriptions, and helper text.
4. Keep only copy that improves understanding or task completion.
5. Re-check tone for AI-style marketing language, em-dash overuse, and over-explanation.

## Output Format

When using this skill for new design work or redesigns, structure the response around:

1. Context
   - product type
   - user goal
   - primary action
2. Key Decisions
   - information hierarchy
   - interaction pattern
   - copy approach
   - visual direction
3. Recommended Changes
   - what to remove
   - what to simplify
   - what to redesign
   - what to preserve
4. Final Direction
   - a short summary of the intended UX and visual direction

For UI reviews, prefer:

- what the screen is trying to do
- the highest-priority problems, usually 3 to 5
- why they matter
- specific fixes
- final anti-slop verdict: pass or revise

For copy refinement, prefer:

- the user task
- the current copy problems
- revised copy
- what was removed or simplified
- final tone check: clear, natural, and product-specific

## Durability Checks

Use these checks to keep the work mature over time rather than merely stylish in the moment.

### 1. Start With User Needs, Then Product Context

Do not optimize for trend language, current visual fashion, or what AI tools commonly generate first.

Start with:

- who the user is
- what they are trying to do
- what the product needs to communicate
- what platform and context they are in

### 2. Do Less, But Do It Better

If a layout, sentence, card, chart, illustration, or effect does not improve comprehension, trust, or task completion, remove it.

Less surface area usually creates:

- clearer hierarchy
- stronger product identity
- less maintenance burden
- fewer accessibility failures

### 3. Be Consistent, Not Uniform

Reuse patterns, language, and interaction logic where that helps users build familiarity.

Do not force every screen into the same visual treatment when the content, task, or context is different.

Consistency should reduce user effort.
Uniformity should not erase meaning.

### 4. Prefer Evidence Over Taste When You Can

If real usage, support feedback, analytics, research, or usability findings exist, let them overrule stylistic preference.

Use judgment when evidence is unavailable, but do not confuse personal taste with product truth.

### 5. Keep the Interface Honest and Maintainable

Do not rely on fake data, decorative dashboards, inflated claims, or interface patterns that only look convincing in a static mockup.

Favor solutions that will still read clearly when the product has:

- empty states
- long labels
- real user content
- failure states
- smaller screens
- future feature growth

### 6. Make the Design Language Systematic

Visual quality should not depend on one lucky screen.

Define a small, explicit system for:

- color roles instead of random per-screen color choices
- typography scale instead of one-off size decisions
- spacing rhythm instead of ad hoc gaps
- component states and variants instead of isolated styling
- motion and emphasis rules instead of decorative effects added late

The goal is not rigidity.

The goal is that the product still feels coherent after the tenth screen, the third contributor, and the next redesign cycle.

### 7. Review Responsive and Accessible Behavior Before Final Polish

A design is not mature if it only works in the most flattering viewport with the shortest content.

Check early for:

- long labels and dense content
- keyboard and focus behavior
- reduced-motion and contrast needs
- touch-target sizing
- empty, loading, and failure states on smaller screens

## References Used To Shape This Guide

This guide is intentionally opinionated, but it aligns with durable ideas from mature design and content systems, especially:

- GOV.UK design principles and content design guidance
- Apple Human Interface Guidelines
- GitHub content design principles and accessibility guidance
- Material Design and Adobe Spectrum guidance on tokens, states, and accessibility

---

# 1. Start With the Product, Not the Aesthetic

Before designing, understand:

- Who is using the product?
- What are they trying to accomplish?
- What is the primary task?
- What information matters most?
- What actions are most important?
- What is the product's personality?
- What makes this product different?
- What platform is it used on?
- What existing design system must be preserved?

Do not start with:

> “Make it modern.”

or:

> “Make it look like an AI product.”

Translate vague aesthetic requirements into concrete design decisions appropriate to the product.

A banking app, music app, ecommerce app, education app, developer tool, and construction app should not all look like the same AI startup.

---

# 2. Make the Interface Obvious Before Making It Explanatory

If the layout, hierarchy, controls, and labels already communicate what the user should do, **do not add explanatory prose**.

Prefer:

> **Upload document**

over:

> Upload your document to begin the intelligent analysis process. Once uploaded, our system will analyze its contents and provide detailed insights.

### Rule

> **Fix confusing interfaces with design before fixing them with prose.**

If a paragraph exists because the UI itself is unclear, improve the UI first.

---

# 3. Design for Scanning

Users should quickly understand:

- What this screen is
- What they can do
- What they should do next
- What happened
- What needs attention

Prefer:

- Strong hierarchy
- Short labels
- Familiar controls
- Grouping
- Whitespace
- Clear primary actions
- Progressive disclosure

Avoid:

- Essay-length UI copy
- Long descriptions beneath every control
- Repeating information already visible
- Excessive helper text
- Every section having a title + subtitle + description
- Turning obvious interactions into instructions

---

# 4. Speak Like the User

Use the simplest accurate language the intended user would naturally use.

| Technical | Human |
|---|---|
| Authenticate | Sign in |
| Configuration | Settings |
| Configure | Set up |
| Parameters | Options |
| Initiate | Start |
| Execute | Run |
| Generate | Create |
| Input | Enter |
| Output | Result |
| Query | Search |
| Processing | Working |
| Integration | Connect |
| Workflow | Steps |
| Deployment | Publish |
| Optimization | Improve |

Technical terminology is appropriate when the audience actually needs it.

The rule is not:

> Never use technical words.

It is:

> **Never use technical language merely because it sounds sophisticated.**

---

# 5. Never Make Consumer UI Sound Like Documentation

Avoid:

> Configure your preferred parameters before initiating generation.

Prefer:

> **Choose your options**

Avoid:

> Upload the required assets to commence processing.

Prefer:

> **Upload files**

The interface should describe **what the user can accomplish**, not the internal architecture of the software.

---

# 6. Every Piece of Copy Must Earn Its Space

For every sentence, ask:

> If I remove this, does the user's ability to understand or complete the task become meaningfully worse?

If no, remove it.

This applies to:

- Headings
- Subtitles
- Cards
- Empty states
- Buttons
- Forms
- Dialogs
- Settings
- Dashboards
- Onboarding

Do not add copy merely because the screen feels empty.

**Whitespace is not a problem that needs to be filled.**

---

# 7. Avoid AI-Generated Writing Patterns

The interface copy should sound like a human product team wrote it for its users.

Avoid repetitive patterns that commonly make generated copy feel artificial.

### Avoid excessive em dashes

Do not repeatedly write:

> Build faster — without compromising quality.

> One platform — everything you need.

> Simple, powerful — and built for you.

An occasional em dash is completely fine.

The problem is **repetitive em-dash-heavy writing across headings, descriptions, and marketing copy**.

Prefer natural sentence structure, shorter sentences, commas, colons, or separate sentences where appropriate.

### Also avoid repetitive AI marketing language

Be skeptical of phrases such as:

- AI-powered
- Intelligent
- Smart
- Seamless
- Next-generation
- Revolutionary
- Transform
- Elevate
- Supercharge
- Unlock
- Effortless
- Cutting-edge
- Powerful yet simple

Use concrete language instead.

### Rule

> **Write like a product team speaking to customers, not like a language model trying to sound polished.**

---

# 8. Use Consumer-Oriented Actions

Describe what the user wants to accomplish, not what the machine does internally.

Prefer:

> **Improve photo**

over:

> AI-powered image enhancement

Prefer:

> **Get an answer**

over:

> Generate a contextually optimized response

Prefer:

> **Organize files**

over:

> Execute automated document classification

The technology is implementation.

The user's goal is the product experience.

---

# 9. Avoid the Stereotypical AI Color Language

Do not automatically default to the stereotypical AI palette:

- Electric blue
- Cyan
- Neon purple
- Magenta
- Blue-on-black
- Purple-on-black
- Cyan/purple neon combinations
- Highly saturated futuristic accents

These colors are not forbidden.

The problem is using them **because they make the product look technological or AI-powered**.

### Prefer

A deliberate, product-specific palette chosen for:

- Brand identity
- Audience
- Industry
- Emotional tone
- Hierarchy
- Accessibility
- Long-term visual quality

For premium products, generally favor **restrained, sophisticated palettes with controlled accent colors** over excessive neon saturation.

Blue is not forbidden.

Purple is not forbidden.

Neon is not forbidden.

The rule is:

> **Do not choose a color because it looks like AI. Choose it because it belongs to the product.**

---

# 10. Neon Test

Before finalizing the palette, ask:

- Is the primary color an unnecessarily saturated electric blue?
- Are cyan, purple, and magenta combined simply because they look “AI”?
- Is the background dark mainly so neon elements can glow?
- Are borders, text, or controls glowing?
- Would reducing saturation make the product feel more refined?
- Does the palette communicate the product or merely “technology”?

If the palette communicates **AI aesthetic rather than product identity**, revise it.

---

# 11. Avoid AI Visual Clichés

Do not automatically reach for:

- Purple/blue/pink gradients
- Gradient text
- Giant gradient blobs
- Aurora backgrounds
- Excessive glow
- Glowing borders
- Glassmorphism everywhere
- Dotted backgrounds
- Particle fields
- Neural-network decoration
- Floating glowing orbs
- Robot/AI imagery
- ✨ sparkles everywhere
- Excessive pill/capsule controls
- Dark futuristic backgrounds

These are not forbidden.

They need a **specific reason to exist**.

Ask:

> Would I still make this decision if AI did not exist?

If the answer is no, reconsider it.

---

# 12. Don't Use Capsules Everywhere

Pills are useful for:

- Tags
- Filters
- Statuses
- Compact selections
- Certain buttons

Do not automatically make every:

- Button
- Input
- Card
- Tab
- Navigation item
- Badge
- Container

a pill.

### Rule

> **Shape should communicate function, not imitate a trend.**

---

# 13. Don't Use Dots Without Meaning

Dotted backgrounds and particle fields are strong AI visual signals.

Use them only when they contribute to:

- Brand identity
- Information
- Spatial guidance
- Product meaning
- Visual structure

If they are purely decorative, remove them.

---

# 14. Give Gradients a Job

Gradients can be excellent.

Use them for:

- Brand identity
- Hierarchy
- Depth
- State
- Focus
- Meaningful emphasis

Do not automatically use:

> purple → pink → blue + blur + glow

because it “looks AI.”

### Rule

> **Do not use effects to compensate for weak hierarchy or weak visual design.**

---

# 15. Use Real Iconography, Not Emoji Substitutes

Functional UI should use a consistent icon system rather than emojis as visual shortcuts.

Prefer:

- Lucide
- Another consistent SVG icon library
- Platform-native icons
- A custom product icon system

For example:

Do not automatically create:

> ⚙️ Settings  
> 📊 Analytics  
> 🔍 Search  
> 🗑️ Delete  
> 📁 Files

Use appropriate UI icons instead.

Emojis are appropriate when they are genuinely part of:

- User-generated content
- Social communication
- Brand personality
- A playful product
- The actual meaning of the content

The rule is:

> **Do not use emojis simply because they are an easy replacement for proper iconography.**

Also avoid mixing random icon styles.

---

# 16. Cards Must Earn Their Existence

Do not turn every piece of information into a rounded card.

Before creating a card, ask:

> Does a bounded container improve grouping, comparison, hierarchy, interaction, or comprehension?

If not, use something simpler:

- Text
- List
- Table
- Section
- Divider
- Inline content
- Navigation

Avoid repetitive:

> card + card + card + card + card

when the content would be clearer without them.

---

# 17. Avoid Centered-Everything Layouts

AI-generated interfaces frequently default to:

- Centered hero
- Centered headline
- Centered subtitle
- Centered buttons
- Centered content
- Symmetrical three-column sections

Center alignment is sometimes correct.

Do not use it as the universal layout.

Choose composition based on:

- Content
- Reading direction
- Hierarchy
- Product context
- User task
- Visual rhythm

---

# 18. Avoid Generic Page Templates

Do not automatically generate:

> Giant hero → two CTAs → three feature cards → testimonials → pricing → final CTA

or:

> Sidebar → top bar → four metric cards → chart → three cards

These structures are useful only when they fit the product.

### Rule

> **Choose information architecture before choosing visual components.**

Two different products should not become the same interface after changing the colors and text.

---

# 19. Don't Invent Content

Never fabricate content simply to make a UI look complete.

Do not invent:

- Statistics
- Metrics
- Testimonials
- Customer logos
- Reviews
- Activity
- Avatars
- Charts
- Notifications
- “Insights”
- Recent items
- Progress
- Usage numbers

If real data is unavailable, design the appropriate:

**empty, loading, placeholder, or example state.**

A truthful empty state is better than fake realism.

---

# 20. Don't Build Decorative Dashboards

Do not add charts, widgets, metrics, activity feeds, or status panels merely because “dashboards should have them.”

Every element must represent:

1. Real information
2. A real state
3. A real action
4. Meaningful navigation

If none apply, remove it.

---

# 21. Make Typography Intentional

Do not blindly default to the most common SaaS font stack.

Typography should be chosen deliberately based on:

- Product identity
- Audience
- Platform
- Readability
- Hierarchy

Using a popular font is fine when appropriate.

The problem is **defaulting without consideration**.

---

# 22. Don't Use Decoration as a Shortcut

Do not add visual elements merely because a screen looks too empty.

Be suspicious of:

- Random lines
- Dots
- Blobs
- Sparkles
- Decorative icons
- Gradient shapes
- Floating objects
- Abstract illustrations
- Unnecessary borders
- Random badges

Ask:

> **Does this communicate something, establish hierarchy, support the brand, or improve the experience?**

If not, remove it.

---

# 23. Don't Make Everything “AI”

Not every feature needs an AI label.

Avoid unnecessary:

- AI Search
- AI Dashboard
- AI Settings
- AI Recommendations
- AI Insights
- AI Assistant
- AI Mode

If AI improves an ordinary feature, the feature can simply be presented as the feature.

The user cares about the result.

---

# 24. AI-Native Interaction Is Different From AI Slop

Do not reject useful AI patterns merely because they are associated with AI.

Valid patterns include:

- Streaming responses
- Copilot panels
- Regeneration
- Suggestions
- Tool activity
- Useful reasoning/status states
- Confidence indicators
- Voice interaction
- Agent progress

Use them when they improve:

- Understanding
- Control
- Feedback
- Trust
- Task completion

Do not add them merely to make the interface appear intelligent.

---

# 25. Keep AI Status Useful

Avoid theatrical states:

> ✨ Activating advanced intelligence...

Prefer useful feedback:

> **Uploading 3 of 8 files…**

> **Searching…**

> **Finding nearby stores…**

> **Preparing your report…**

Show the user what matters rather than performing intelligence for them.

---

# 26. Progressive Disclosure

Do not expose the entire system to the user.

Hide complexity until it is useful.

Prefer:

> **Advanced settings**

over immediately exposing:

- Model
- Temperature
- Context
- Tokens
- Retrieval
- Tools
- Reasoning
- Parameters

Advanced controls should exist when useful, but should not become mandatory knowledge.

---

# 27. Use Familiar Interaction Patterns

Prefer established patterns when they solve the problem well:

- Search
- Lists
- Tables
- Tabs
- Menus
- Forms
- Checkboxes
- Toggles
- Dropdowns
- Modals
- Sidebars
- Pagination

Do not invent interactions simply to appear innovative.

### Principle

> **Innovation should improve the task, not merely the screenshot.**

---

# 28. One Clear Primary Action

Each screen should have a clear hierarchy.

Identify:

**Purpose:** What is this screen for?

**Primary action:** What should the user most likely do?

**Secondary actions:** What else can they do?

**Information:** What must they know?

Do not make every button equally prominent.

---

# 29. Design the Edge Cases

A UI is not complete when the happy path looks good.

Consider:

- First use
- Empty state
- Loading
- Success
- Error
- No results
- Long content
- Long names
- Missing data
- Permissions
- Offline/failed requests
- Small screens
- Large screens
- Keyboard interaction
- Accessibility

Design these intentionally rather than leaving them for later.

---

# 30. Preserve Existing Product Identity

When modifying an existing application:

1. Inspect the current design system.
2. Understand its typography.
3. Understand its colors.
4. Understand spacing and components.
5. Understand existing interaction patterns.
6. Preserve established conventions unless there is a reason to change them.

Do not redesign an existing product into the agent's favorite AI aesthetic.

**Consistency is more important than novelty.**

---

# 31. Responsive and Accessible by Default

Anti-AI-slop is not purely visual.

The interface must remain usable across:

- Mobile
- Tablet
- Desktop
- Different viewport sizes
- Keyboard navigation
- Screen readers
- Different text sizes

Ensure:

- Adequate contrast
- Visible focus states
- Usable touch targets
- Clear hierarchy
- Logical keyboard order
- Meaningful labels
- Motion that does not harm usability

A visually distinctive interface that is difficult to use is still a bad interface.

---

# 32. Product Specificity Test

Ask:

> Could I change the logo, colors, and text and use this exact design for a completely different company?

If yes, it is probably too generic.

The interface should contain decisions that come from:

- The product
- The audience
- The domain
- The workflow
- The brand
- The actual information

---

# 33. Five-Second Test

Pretend the user has never seen the product.

Give them five seconds.

Can they identify:

1. What is this?
2. What can I do here?
3. What should I do first?
4. What happens when I take the primary action?

If not, **do not immediately add more copy.**

First improve:

- Hierarchy
- Layout
- Labels
- Grouping
- Contrast
- Placement
- Information architecture

---

# 34. Remove 30%

After completing a screen, deliberately try to remove approximately 30% of its elements.

Look for:

- Redundant labels
- Duplicate information
- Decorative elements
- Unnecessary descriptions
- Excessive badges
- Unnecessary icons
- Repeated headings
- Redundant buttons
- Excessive borders
- Unnecessary cards
- Fake dashboard content

If removing something improves clarity, keep it removed.

Do not add things back simply because the screen now feels “empty.”

---

# 35. Final Anti-Slop Review

Before delivering the UI, critique it across six dimensions.

### Intent

- Is the design clearly derived from the product?
- Is there a deliberate visual direction?
- Does the design fit the audience?

### Hierarchy

- Is the primary action obvious?
- Can the interface be scanned quickly?
- Is important information visually prioritized?

### Specificity

- Does this feel like this product?
- Could the same interface belong to another company?
- Did the design avoid generic templates?

### Restraint

- Does every element earn its space?
- Are cards necessary?
- Are gradients necessary?
- Are decorative effects necessary?
- Can anything be removed?

### Human UX

- Is the language natural?
- Are technical terms necessary?
- Does the user understand what to do without an essay?
- Are familiar interaction patterns used?
- Are edge cases handled?

### AI-Slop

- Does it rely on stereotypical AI aesthetics?
- Does it use neon blue/cyan/purple simply to look technological?
- Does it look like a generic AI SaaS template?
- Are there unnecessary sparkles, gradients, pills, dots, glow, or glass?
- Are emojis being used where proper icons should be used?
- Is the copy unnaturally heavy on em dashes?
- Is there fake content?
- Is the interface over-explaining itself?
- Does the visual language feel interchangeable with other AI products?

If several appear together, redesign rather than merely tweaking them.

---

# 36. Revision Gate

Do not stop at critique.

If the review identifies:

- Genericity
- Weak hierarchy
- Unnecessary decoration
- Excessive copy
- AI-like writing patterns
- Fake content
- Poor product specificity
- Unnecessary complexity
- Accessibility problems
- Responsive problems
- AI-looking color choices
- Generic visual language
- Emoji-based UI shortcuts
- Excessive em-dash usage

**Revise the design before delivering it.**

The goal is not to produce a design that technically follows the rules.

The goal is to produce a design that **feels deliberately designed**.

---

# Final Principle

The best AI interface does not constantly announce that it is AI.

AI should increasingly **disappear into the product**.

Instead of:

> ✨ AI Recommendations

use:

> **Recommended for you**

Instead of:

> ✨ AI Image Enhancement

use:

> **Improve**

Instead of:

> ✨ AI Assistant

sometimes simply provide:

> **Search**

or:

> **Help**

The technology is not the experience.

**The product is the experience.**

---

# Agent Directive

When designing or reviewing a UI:

**Understand the product → establish intent → choose information structure → establish hierarchy → choose visual language → implement → test edge cases → run anti-slop review → remove unnecessary elements → revise → deliver.**

Never start from a collection of fashionable UI components.

Never optimize for a screenshot at the expense of usability.

Never add complexity to prove sophistication.

Never add explanation when better design would make it unnecessary.

Never fabricate content to make a product look complete.

Never choose a visual pattern merely because AI systems commonly choose it.

Never use emojis as a shortcut for proper functional iconography.

Never overuse em dashes to manufacture polished-sounding copy.

Never default to neon blue, cyan, purple, or futuristic palettes merely because they communicate “AI.”

When deciding between:

- More explanation vs clearer design → **clearer design**
- Technical wording vs everyday wording → **everyday wording**
- Decoration vs whitespace → **whitespace**
- Generic template vs product-specific composition → **product-specific composition**
- More cards vs simpler information structure → **simpler structure**
- Fake completeness vs truthful emptiness → **truthful emptiness**
- Novel interaction vs familiar interaction → **familiar interaction**
- More controls vs progressive disclosure → **progressive disclosure**
- Generic AI aesthetic vs product identity → **product identity**
- Neon technology aesthetic vs refined product palette → **refined product palette**
- Emoji shortcut vs proper iconography → **proper iconography**
- Elaborate explanation vs obvious interface → **obvious interface**
- “Looks impressive” vs “is immediately understandable” → **immediately understandable**

The final interface should be:

**Minimal without being empty.  
Modern without being trend-dependent.  
Premium without being ornamental.  
Distinctive without being decorative.  
Intelligent without constantly announcing its intelligence.  
Specific to its product rather than interchangeable.  
Human in its language and interaction.  
And clear enough that the user rarely needs instructions.**
