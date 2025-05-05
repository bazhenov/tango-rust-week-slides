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
mdc: true
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
layout: center
---

# **Solution:** Control as much as you can

- disable SMT / DVFS / Power Saving
- core / NUMA / IRQ pinning
- randomize everything else: vmap/stack allocation

---
layout: center
---

# ...well, kind of 🫤

<style>
h1 {
    font-size: 5rem
}
</style>

---
layout: center
---

# ✅ Better solution

## Run **2 algorithms** you want to compare _simultaneously_

By calculating [candidate]{.candidate}-[baseline]{.baseline}, most common mode noise will be _automatically eliminated_.

<style>
h2 {
    padding: 2rem 0;
}
.baseline {
    color: darkgreen;
    font-weight: bold;
}
.candidate {
    color: darkred;
    font-weight: bold;
}
</style>

---
layout: image
image: /images/img1.svg
backgroundSize: 90% 90%
---

---
layout: image
image: /images/img2.svg
backgroundSize: 90% 90%
---

---
layout: statement
---

# ⏱️
# Performance is <v-mark>only</v-mark> <nobr>short-term</nobr> predictabile

---
layout: image
image: /images/vcs.svg
backgroundSize: 90% auto
---

---
layout: image
image: /images/scheme.svg
backgroundSize: auto 90%
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
