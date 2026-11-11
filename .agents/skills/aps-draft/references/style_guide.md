# APS Draft Style & Speech Guide

This guide details the sentence structures, tone, and stylistic traits observed in the user's existing APS preparation drafts in `drafts/`.

---

## 1. Voice and Perspective

- **Perspective**: First person plural (*"we learned"*, *"we covered"*, *"we mainly focused on"*) or first person singular (*"I would talk about..."*, *"I would draw a structure showing..."*, *"I modified the register..."*).
- **Tone**: Professional, confident, and explanatory oral English. Not overly conversational slang, but also not stiff written literature.
- **Goal**: Make it effortless for the student to look at the draft, memorize key talking points, and verbalize them smoothly when the German interviewer asks *"Tell me about this course"*.

---

## 2. Signature Sentence Patterns from Existing Drafts

### Course Overview & Motivation
- *"In this course, we learned [Topic]. That's on the [e.g., Application/Communication/Perception] layer of [e.g., IoT 3-layer model / OSI stack] because [Reason]."*
- *"[Course/Topic] means [Full definition]. In this course, we mainly focused on [Core areas]."*
- *"We covered these topics: 1. ..., 2. ..., 3. ... "*

### Transitioning Between Concepts
- *"Before getting into [B], I would talk about [A] first because [A] is the basis of running..."*
- *"Then, the next topic / peripheral: [Name]. [Name] is used to [function]..."*
- *"Different from the [Traditional approach], [New approach] adopts [Feature]. The most significant difference is..."*

### Tradeoffs and Comparisons (Key APS Interview Focus)
- *"There are 2 kinds of [X] we covered: [A] and [B]. They are quite different: ..."*
- *"We chose [X] but not [Y] because [X] needs only [advantage], whereas [Y] requires [tradeoff]. In resource-restricted systems, bandwidth/memory usage is critical."*
- *"The difference between [A] and [B] is the rendering range: for [A], only dirty rectangles are refreshed; for [B], the entire frame is refreshed constantly."*

### Drawing Cues (Crucial for APS Whiteboard / Scratch Paper)
- *"I would like to draw a picture showing how [X] works:"*
- `<drawing the PWM working graphic>`
- `![image.png](Course/image.png)`
- ASCII flowcharts connecting registers, clocks, or layer stacks.

### Lab & Experiment Narrative
- *"In our lab lectures, we used [Tool, e.g. Cisco Packet Tracer / STM32CubeMX / Keil / VSCode] to complete two practical tasks: [Task 1] and [Task 2]."*
- *"We took the experiment of [Task]:"*
  - *"Modify [file.c / register] to implement [feature]."*
  - *"Connect [Device A] to [Device B] via [Serial Port / JTAG / Cable]."*
  - *"In [Simulator/Tool], switch from Realtime Mode to Simulation Mode..."*
  - *"Observation: [What happened, e.g. LED blinked, packet captured, serial output verified the topology]."*

---

## 3. Explaining Technical Abbreviations
Always give the full name followed by a short plain-English explanation before diving into details:
- **MCU**: Microcontroller Unit (Core + Memory + Peripherals)
- **GPIO**: General Purpose Input/Output
- **SAR ADC**: Successive Approximation Register Analog-to-Digital Converter
- **LVGL**: Light and Versatile Graphics Library
- **DMA**: Direct Memory Access (data transfer without CPU overhead)
- **LTDC**: LCD-TFT Display Controller
