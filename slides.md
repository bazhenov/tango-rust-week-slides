---
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Tango – Rust Week 2025
info: |
  ## Tango
  Precise Performance Measurement through Direct Comparison
class: text-center
drawings:
  persist: false
transition: slide-up
---

# Tango

Precise Performance Measurement through Direct Comparison

<!--
Thank people.

Thank organizers.

Introduce myself. I'm intrested in benchmarking.

Introduce a novel way of measuring performance.
-->

---
transition: slide-up
---

# How do we measure performance?

```rust {3-5|2,6}
fn measure(f: impl Fn()) -> u64 {
    let start = Timer::now();
    for _ in 0..iterations {
        black_box(f());
    }
    Timer::now() - start
}
```

<style>
code {
  font-size: 200%;
}
</style>

<!--
-->

---

# Wrong assumptions 🙅‍♂️

Performance measurements are **not** independent **nor** they identically distributed.

| System Level | Examples |
| --- | --- |
| Hardware | DVFS, Power Management, SMT, i/d cache invalidation, i/d alignment |
| OS | paging, interrupt handling, NUMA allocation, task scheduling |
| Runtime | JIT, GC, task scheduling |

<style>
th {
    font-weight: bold;
}
</style>

---

# Solution

## Control as much as you can <v-click>🫤</v-click>

- disable SMT/DVFS/Power Saving
- core/NUMA/IRQ pinning
- randomize everything else

<v-after>

## ✅ Run both algorithm you want to compare simultaneously

By subtracting one measurement from the other, most common mode noise in the measurements will be automatically eliminated.

</v-after>

<style>
h2 {
    padding: 2rem 0;
}
</style>

---
layout: image
image: /images/img1.svg
backgroundSize: contain
---

---
layout: image
image: /images/img2.svg
backgroundSize: contain
---

---
layout: statement
---

# ⏱️
# Performance short-term predictability

---
layout: image
image: /images/vcs.svg
backgroundSize: contain
---

---
layout: two-cols-header
---

<center>
    <h1>Thank you</h1>
</center>

::left::

<img class="h-full w-100" src="/images/qr.svg" />

::right::

## Denis Bazhenov

- <nobr><mdi-github /> <a href="https://github.com/bazhenov/tango">https://github.com/bazhenov/tango</a></nobr>
- <nobr><mdi-web /> <a href="https://bazhenov.me/posts">https://bazhenov.me/posts</a></nobr>

<style>
    img {
        background-color: white;
    }

    ul {
        list-style-type: none;
        padding: 2rem 0;
        margin: 0;
        font-size: 1.5rem;
    }
    li {
        padding: 0;
        margin: 0;
    }

</style>
