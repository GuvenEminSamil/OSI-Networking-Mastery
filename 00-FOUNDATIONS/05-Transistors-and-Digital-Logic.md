# 00-05 — Transistors and Digital Logic

> **Prerequisite:** 00-03 — Binary Arithmetic and Boolean Logic  
> **CCNA connection:** Understanding the basic hardware inside network devices and how Cisco devices store configuration files.  
> **Suggested study time:** Flexible.

## What You Will Learn

- Understand what a transistor does in a digital device.
- Recognize how logic gates are built from electronic switches.
- Understand the basic difference between RAM, ROM, NVRAM, and flash.
- Save a Cisco device's configuration so it remains after a restart.

You do not need to study transistor physics or chip design in detail for the CCNA exam. Focus on the practical ideas in this lesson.

## 1. What Is a Transistor?

A **transistor** is a small electronic component that can control the flow of electrical current. In digital devices, it can work like a very fast switch.

A normal light switch is controlled by your hand. A transistor can be controlled by an electrical signal and can change state extremely quickly.

Modern processors and network devices contain very large numbers of transistors. They use them to build logic circuits and memory.

A common type is a **MOSFET** (Metal-Oxide-Semiconductor Field-Effect Transistor). It uses voltage at its control terminal to regulate current. You only need to remember its role here: it can act as an electronic switch.

## 2. From Transistors to Logic Gates

A **logic gate** is a small circuit that performs a Boolean operation on one or more input bits.

You have already seen these operations in 00-03:

- AND
- OR
- NOT
- NAND
- NOR
- XOR

Transistors are combined to create these gates. Gates are then combined to create larger circuits such as processors, counters, and network-device hardware.

For example, a NOT gate reverses its input:

| Input | Output |
|---:|---:|
| 0 | 1 |
| 1 | 0 |

The important idea is not the transistor-level circuit. It is that digital hardware processes information by applying logical operations to bits.

## 3. How Does a Device Remember Information?

A computer needs memory to store information while it works.

**RAM** (Random Access Memory) is temporary working memory. It is usually **volatile**, which means its contents are lost when power is removed.

**ROM** (Read-Only Memory) is non-volatile memory used for essential startup instructions. *Non-volatile* means it retains information without power.

Network devices may also use these storage areas:

| Memory | Main purpose | Keeps data without power? |
|---|---|---|
| RAM | Running system, active processes, temporary data | No |
| ROM | Basic startup instructions | Yes |
| NVRAM | Startup configuration on many Cisco devices | Yes |
| Flash | IOS image and files | Yes |

**IOS** means Internetwork Operating System. It is Cisco's network-device operating system.

The exact hardware arrangement can vary by device model. For CCNA fundamentals, learn the roles shown in the table.

## 4. Running Configuration and Startup Configuration

Cisco devices have two configuration views that are especially important.

**Running configuration** is the configuration currently being used by the device. It is held in RAM.

**Startup configuration** is the saved configuration that the device loads when it starts. On many Cisco devices, it is stored in NVRAM.

This explains a common beginner mistake: making a configuration change but not saving it.

Example:

```
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# end
R1# show running-config
R1# show startup-config
```

The running configuration now contains the hostname `R1`. The startup configuration may still contain the old hostname.

To save the current configuration:

```
R1# copy running-config startup-config
Destination filename [startup-config]?
Building configuration...
[OK]
```

The device can now load the saved configuration after a restart.

## 5. Practical Cisco Exercise

Use a router in Cisco Packet Tracer.

1. Open the router's CLI (Command-Line Interface, the text-based way to enter commands).
2. Enter privileged EXEC mode with `enable`.
3. Enter configuration mode with `configure terminal`.
4. Change the hostname to `R1`.
5. Exit configuration mode with `end`.
6. Compare `show running-config` and `show startup-config`.
7. Save using `copy running-config startup-config`.
8. Check both configuration views again.

Before each command, predict what you expect to see.

## 6. Common Mistakes

| Mistake | Correct idea |
|---|---|
| RAM keeps information after power is removed. | RAM is volatile; its contents are lost without power. |
| Running configuration is always saved automatically. | Save it to startup configuration when you want it to survive a restart. |
| Flash and RAM have the same role. | RAM is working memory; flash stores files such as an IOS image. |
| A router's internal transistor design must be memorized for CCNA. | Focus on device behavior, memory roles, and configuration commands. |

## 7. Knowledge Check

1. What is a transistor used for in digital devices?
   <details><summary>Answer</summary>It can act as a very fast electronic switch and help build logic circuits.</details>

2. What does volatile mean?
   <details><summary>Answer</summary>Information is lost when power is removed.</details>

3. Which memory normally holds the running configuration?
   <details><summary>Answer</summary>RAM.</details>

4. What is the purpose of startup configuration?
   <details><summary>Answer</summary>It stores the configuration that the device loads when it starts.</details>

5. Which command saves the running configuration as the startup configuration?
   <details><summary>Answer</summary>`copy running-config startup-config`.</details>

6. What is flash commonly used to store on a Cisco router?
   <details><summary>Answer</summary>The IOS image and other files.</details>

## 8. CCNA Takeaways

- Transistors act as electronic switches inside digital devices.
- Logic gates perform operations on bits.
- RAM is volatile working memory.
- ROM and flash are non-volatile.
- Running configuration is the active configuration.
- Save important changes with `copy running-config startup-config`.

## Self-Check

- [ ] I can describe the role of a transistor in simple words.
- [ ] I can distinguish RAM, ROM, NVRAM, and flash.
- [ ] I can explain the difference between running configuration and startup configuration.
- [ ] I can save a Cisco configuration and verify that it was saved.

**Next lesson:** 00-06 — Data Representation.
