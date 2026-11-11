---
name: aps-draft
description: >-
  Generates, standardizes, and refines oral APS interview course drafts in drafts/<course_name>.md.
  Mimics the user's established style in drafts/ (First-person spoken English, Theory + Lab structure).
  Works whether the user provides course notes (e.g., from notes/) or only provides a course title
  (reconstructing realistic university curriculum and lab experiments).
---

# APS Course Draft Writer & Refiner (`aps-draft`)

This skill guides the agent to produce high-quality, standardized course preparation drafts for the **APS (Akademische Prüfstelle) interview** in `drafts/<course_name>.md`. 

Every draft must emulate the exact tone, style, and structural conventions found in the user's existing drafts (e.g., `drafts/arm_arch.md`, `drafts/computer_networks.md`, `drafts/embedded_gui.md`, `drafts/mcu_principle.md`, `drafts/iot_communication.md`).

---

## 1. Core Principles of APS Drafts

1. **First-Person Spoken English (Oral-Ready)**:
   - Drafts are meant to be spoken aloud to a German interviewer, not read like a research paper.
   - Use spoken opening and transition phrases:
     - *"In this course, we learned..."*
     - *"This course is located at the ... layer of ... hierarchy."*
     - *"Before getting into ..., I would talk about ... first because..."*
     - *"We mainly focused on..."*
     - *"I would like to draw a structure/diagram showing..."*
   - Keep sentences clear, punchy, and grammatically direct. Avoid overly complex subordinate clauses that are difficult to say smoothly during an interview.

2. **The "Two-Pillar" Structure (Theory + Lab)**:
   - German interviewers almost always ask two questions:
     1. *"What is the theoretical principle of [Topic]?"*
     2. *"What experiments or projects did you do in the laboratory?"*
   - Every draft **MUST** have both:
     - **Theory / Core Knowledge**: 3 to 5 core concepts, hierarchical context, comparison points.
     - **Laboratory / Project**: Concrete hands-on experiments with software/hardware tools, configuration steps, and observable results.

3. **Tradeoffs & "Interviewer Baits"**:
   - Explicitly highlight engineering tradeoffs (why choice A was made over choice B):
     - e.g., RGB565 vs RGB888 (bandwidth/RAM vs color depth).
     - Harvard vs Von Neumann (separate bus for speed vs shared bus).
     - TCP vs UDP (reliability vs latency).
     - Polling vs Interrupt (CPU utilization vs responsiveness).
   - These tradeoffs demonstrate genuine engineering understanding and guide the interviewer's follow-up questions to topics the student is prepared for.

4. **Visual & Interaction Cues**:
   - Include drawing placeholders where sketching helps explain concepts on paper during the interview (e.g., `![image.png](...)`, `<drawing the PWM working graphic>`, ASCII block diagrams).

---

## 2. Input Scenarios & Workflow

When invoked to write or update a draft:

### Scenario A: User provides notes or source material
- User points to a file in `notes/` (e.g. `notes/front_end.md`), pastes text, or provides syllabus points.
- **Workflow**:
  1. Inspect the source notes to extract the main theoretical topics, key formulas/architectures, and any mentioned lab experiments.
  2. Filter out unnecessary trivia and retain the core technical principles.
  3. Transform the technical notes into the spoken draft format below.

### Scenario B: User only provides the course name (no notes provided)
- User asks for a draft like "帮我写一下数字信号处理 (DSP) 的 draft" or `drafts/front_end.md` with no notes.
- **Workflow**:
  1. Reconstruct a typical, realistic undergraduate engineering curriculum for that course (aligned with Chinese/German engineering programs).
  2. Select 3-4 foundational theoretical topics with depth.
  3. Formulate 1-2 realistic, standard university laboratory experiments (specifying standard software/hardware tools such as MATLAB, Keil, Packet Tracer, VSCode, Modelsim, etc.).
  4. Consult [course_lab_catalog.md](./references/course_lab_catalog.md) if needed for standard lab setups.

---

## 3. Standard Draft Markdown Template

All generated drafts in `drafts/<course_name>.md` must adhere to this template:

```markdown
# [Course Title]

[1-2 introductory sentences stating the scope, positioning in the overall knowledge hierarchy (e.g., IoT 3-layer model, embedded system stack), and the main tools or simulators used.]
We covered these topics:
1. [Topic 1]
2. [Topic 2]
3. [Topic 3]
4. [Topic 4]

## 1. [Topic 1 Title / or ## Theory]

### [Sub-concept 1.1]
[Explanation with clear bullet points, bold key terms, and definitions]

### [Sub-concept 1.2: Trade-off / Comparison]
[Comparison between two protocols, architectures, or algorithms, e.g., X vs Y]
- **X**: [Key feature, pros, cons]
- **Y**: [Key feature, pros, cons]

## 2. [Topic 2 Title]
...

## [N]. Laboratory / Lab

In our lab lectures, we used **[Software / IDE / Hardware Platform, e.g., VSCode, STM32CubeMX, Cisco Packet Tracer, Wireshark]** to complete [1-2] practical tasks: **[Task 1 Name]** and **[Task 2 Name]**.

### 1. [Task 1 Name]
We took the experiment of [Goal/Objective]:
- [Specific configuration, parameter, or code modified]
- [Step-by-step procedure]
- [Result / Observation: e.g., "The LED blinked when...", "In Wireshark, the 3-way handshake packets SYN, SYN-ACK, ACK were captured."]

### 2. [Task 2 Name]
[Repeat structure for second lab experiment]
```

---

## 4. Quality Checklist before Finalizing

Before completing any draft, verify:
- [ ] Is the file saved in `drafts/<course_name>.md`?
- [ ] Does it have an introductory overview explaining the course role?
- [ ] Are there 3-5 distinct theoretical focus areas with bolded technical terms?
- [ ] Does it contain at least one comparison/tradeoff analysis (e.g., A vs B)?
- [ ] Does it include a dedicated **Laboratory** section with realistic tools, parameters, steps, and observable results?
- [ ] Is the English natural, spoken, and suitable for verbal explanation in an interview?
- [ ] Does the technical depth match a 3rd/4th year university undergraduate level?

---

## 5. Supporting References

- Detailed stylistic conventions & oral phrases: [style_guide.md](./references/style_guide.md)
- Typical course & laboratory database: [course_lab_catalog.md](./references/course_lab_catalog.md)
