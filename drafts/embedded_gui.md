# Embedded GUI: LVGL
In this course, we learned the GUI of Embedded System: LVGL. That's on the Application layer of IoT 3-layer model because LVGL shows the perceive layer data on GUI or screen. We develop that on VSCode LVGL simulator.
We covered these topics:  
1. The hardware and software: ARM MCU and LVGL
2. The Rendering mechanism of LVGL
3. The core engine of LVGL
4. Event-Driven and Objects

## 1. Hardware and Software (ARM MCU & LVGL)

### Memory
The Memory System of ARM includes: Flash, Internal SRAM, External RAM. They plays different roles on LVGL. 
1. Flash: Flash stores the LVGL code, fonts and images.
2. SRAM: SRAM keeps the LVGL memory pool. And Partial Double Buffer located here.
3. External RAM: External RAM keeps the Full-Frame Double Buffer because of its high capacity need.

### Display Categories
There're 2 kinds of display we covered: Display with internal MCU and GRAM (VRAM) and Bare Display. They're quite different: 
1. Display with internal MCU and VRAM  
    - Buffer: Partial Double Buffers
    - Interface: LTDC (Peripheral of MCU, Display Controller)
2. Bare Display  
    - Buffer: Full-Frame Double Buffers
    - Interface: SPI or 8080 Parallel Interface  

### Pixel Format
The Pixel format standard determines the screen color effect. We chose the RGB565 but not RGB888 because RGB565 needs only 2 Bytes for each pixel and RGB888 needs 3 Bytes. Though it have better color, the badwidth usage is more significant in resource restricted MCU. 

## 2. LVGL Rendering

### Buffer Strategy
I mentioned the 2 different Buffer Strategies: Partial and Full-Frame Buffer. The most significant difference b/t them is the rendering range: For Partial, The areas of screen need to be refreshed are labeled as "dirty rectangles", CPU only renders the rectangles; For Full-Frame, CPU renders the entire screen constantly. In LVGL, we mainly used the Partial Double Buffers.
The meaning of "Double" is there're 2 buffers in SRAM: they alternately receiving the CPU rendering data and supporting the access for DMA. This mechanism is called "Ping-Pong Buffering".  

### Dirty Rectangle
Actions trigger the callback function and it labels the "dirty rectangles" to be rendered. Dirty Rectangle and Partial Buffering cooperates to drive display with MCU and VRAM.

### Fonts and Images Pre-rendering
The rendering of fonts and images causes high overhead, it's not good in resource restricted MCU. So there's a mechanism called pre-rendering: The host PC pre-render the fonts and images to bitmaps or pixel arrays.

## 3. LVGL Core Engine
I would like to draw a picture showing how does LVGL core engine work.
```
        MCU TIM: Interrupt
                | lv_tick_inc(1)
                ▼
 Support Timebase for lv_timer_handler()
                  |   (Periodically)    |
                  ▼                     ▼
            1. read_cb()            2. Check dirty rectangle
                  |                       |(Y)          |(N)
                  ▼                       ▼             ▼
             If pressed?         Add into CPU          Done.
           |(Y)        (N)|     rendering queue
           ▼              ▼            |
       Record the    Record last       ▼
       coordinate    coordinate     Rendering
                   |                   |
                   ▼                   ▼
              Hit Testing           flush_cb()
            |(Y)          |(N)      
            ▼             ▼
       Dispatch          Done.
       Event.
```

## 4. Event-Driven and Obj.

### Event-Driven: Observer Mode
Event-Driven is different to the convensional function calling. We need to register the event with callback function. As the event triggered, the callback function would be called automatically. LVGL uses the mechanism so we need to register event for the widgets.

### Widget
To create a widget, we need to:
1. Create the widget and assign parent
2. Adjust the size and alignment
3. Customize the style
4. Register the event