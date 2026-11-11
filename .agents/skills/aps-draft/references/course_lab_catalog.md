# University Engineering Course & Lab Catalog (APS Standard)

This reference contains typical undergraduate engineering courses (IoT, Embedded Systems, Computer Science, Electronics) along with their standard university laboratory experiments and software/hardware platforms. Use this catalog when the user requests a draft without providing existing notes.

---

## 1. Web Front-End Development (`front_end.md`)
- **Hierarchy**: Application Layer / Presentation Layer in Web & IoT architectures.
- **Theory Core**:
  - **HTML5**: Semantic tags (`<header>`, `<nav>`, `<article>`, `<footer>`), DOM tree structure.
  - **CSS3 Layouts**: Box model (margin, border, padding, content), Flexbox (`display: flex`, `justify-content`, `align-items`), Grid layout, Responsive design (`@media` queries).
  - **JavaScript Core**: Event-driven model, asynchronous execution (Event Loop, Callback, Promise, `async/await`), DOM manipulation (`querySelector`, `addEventListener`), AJAX / `fetch` API.
- **Laboratory**:
  - *Tool*: VSCode, Chrome DevTools, Live Server.
  - *Lab 1 (Responsive Dashboard)*: Build a responsive IoT sensor display card using HTML5 and CSS Flexbox layout; test viewport resizing.
  - *Lab 2 (Async Data Fetching & DOM Rendering)*: Use JavaScript `fetch()` to call a RESTful API (or mock JSON data), dynamically parse JSON, and update the sensor data table in the DOM without reloading the page.

---

## 2. Operating Systems (`operating_systems.md`)
- **Hierarchy**: System Software layer between Hardware and Applications.
- **Theory Core**:
  - **Process Management**: Process states (Ready, Running, Blocked), PCB (Process Control Block), Context Switch, CPU scheduling (FCFS, Round Robin, Priority).
  - **Synchronization & Concurrency**: Critical Section, Race Conditions, Mutex, Semaphores (`wait()` / `signal()`), Deadlock (4 necessary conditions, prevention & Banker's algorithm).
  - **Memory Management**: Virtual Memory, Paging vs Segmentation, Page Table, TLB, Page replacement algorithms (FIFO, LRU).
  - **File System**: Inode structure, file allocation methods.
- **Laboratory**:
  - *Tool*: Ubuntu Linux / GCC / GDB or xv6.
  - *Lab 1 (Process Creation & IPC)*: Implement multi-process communication using `fork()`, `pipe()`, or POSIX shared memory (`shmget`), synchronizing with semaphores.
  - *Lab 2 (Custom Thread Pool / Producer-Consumer)*: Write a C program using POSIX threads (`pthread`) with mutex lock and condition variables to solve the producer-consumer buffer problem.

---

## 3. Database Systems (`database_systems.md`)
- **Hierarchy**: Data persistence & Information Management layer.
- **Theory Core**:
  - **Relational Model**: E-R Diagrams, Relational Algebra, Normalization (1NF, 2NF, 3NF, BCNF) to reduce data redundancy and anomalies.
  - **SQL**: DDL, DML, complex JOINs (Inner, Left, Right), subqueries, aggregations (`GROUP BY`, `HAVING`).
  - **Transactions & ACID**: Atomicity, Consistency, Isolation, Durability; Concurrency anomalies (Dirty read, Non-repeatable read, Phantom read); Transaction isolation levels.
  - **Indexing & Storage**: B+ Tree index structure, Hash index, Clustered vs Secondary indexes.
- **Laboratory**:
  - *Tool*: MySQL / Navicat / PostgreSQL.
  - *Lab 1 (Database Design & SQL Queries)*: Design an E-R schema for a student management / smart home system, generate DDL, write multi-table JOIN queries and views.
  - *Lab 2 (Transaction Isolation & Index Optimization)*: Use `EXPLAIN` to analyze query execution plans before and after adding a B+ Tree index; demonstrate concurrency isolation levels using two concurrent MySQL terminal sessions.

---

## 4. Digital Signal Processing (`dsp.md`)
- **Hierarchy**: Perception & Signal Processing layer.
- **Theory Core**:
  - **Sampling & Reconstruction**: Nyquist-Shannon sampling theorem, Aliasing effect, ADC quantization.
  - **Transforms**: DTFT (Discrete-Time Fourier Transform), DFT (Discrete Fourier Transform), FFT (Fast Fourier Transform radix-2 decimation-in-time algorithm).
  - **Filter Design**: FIR (Finite Impulse Response, linear phase, window method) vs IIR (Infinite Impulse Response, bilinear transformation, Butterworth / Chebyshev).
- **Laboratory**:
  - *Tool*: MATLAB / TI DSP CCS (Code Composer Studio) with TMS320.
  - *Lab 1 (FFT Spectrum Analysis)*: Generate a dual-frequency sinusoidal signal in MATLAB, compute and plot its 64-point/128-point FFT spectrum, observe spectral leakage.
  - *Lab 2 (FIR Low-Pass Filter Design)*: Design an FIR low-pass filter using the Hamming window method in MATLAB to filter out high-frequency noise from an audio/sensor signal.

---

## 5. Principles of Electronic Circuits / Analog Circuits
- **Hierarchy**: Physical / Hardware Circuit layer.
- **Theory Core**:
  - **Semiconductor Devices**: Diode characteristics, BJT (Bipolar Junction Transistor) operating regions (Cutoff, Active, Saturation), MOSFET (Enhancement-mode NMOS).
  - **Amplifier Circuits**: Common-Emitter (CE) amplifier, small-signal equivalent circuit model, Voltage gain ($A_v$), Input impedance ($R_{in}$), Output impedance ($R_{out}$).
  - **Operational Amplifiers (Op-Amp)**: Virtual short and virtual ground principles, Inverting / Non-inverting amplifiers, Voltage follower, Differential amplifier, Active filters.
  - **Negative Feedback**: 4 feedback topologies (voltage/current series/shunt), gain stabilization, bandwidth extension.
- **Laboratory**:
  - *Tool*: Multisim / LTspice / Breadboard + Oscilloscope + Signal Generator.
  - *Lab 1 (Single-Stage BJT CE Amplifier)*: Measure quiescent operating point ($Q$-point), input a 1kHz sine wave, measure voltage gain and demonstrate output waveform clipping distortion when adjusting base resistor.
  - *Lab 2 (Op-Amp Mathematical Circuit)*: Construct an inverting amplifier and summing amplifier using $\mu$A741 / LM358, measure input-output waveforms on an oscilloscope.
