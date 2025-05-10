---
theme: seriph
# some information about your slides (markdown enabled)
title: Tango – Rust Week 2025
info: |
  ## Tango
  Precise Performance Measurement through Direct Comparison
class: text-center
drawings:
  persist: false
transition: fade
layout: intro
mdc: true
aspectRatio: 16/9
---

# Tango

Precise Performance Measurement<br/> through Paired Benchmarking

<!--
Thank people.

Thank organizers.

Introduce myself. I'm intrested in benchmarking.



Introduce a novel way of measuring performance.
-->

<style>
.slidev-layout {
    background: url("/images/bg.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    background-color: black;

    h1 {
        color: white
    }

    p {
        color: white;
    }
}
</style>

---
layout: full
---

# How do we measure performance?

```rust {3-5|2,6}{at:2}
fn measure(f: impl Fn()) -> u64 {
    let start = Timer::now();
    for _ in 0..iterations {
        algorithm_of_intrest();
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

Some factors you [can control]{.green}, others only [under specific conditions]{.yellow}, others are [impossible]{.red} to control.

| System Level | Examples |
| --- | --- |
| Hardware | [DVFS]{.yellow}, [TDP]{.red}, [SMT]{.yellow}, [i/d cache invalidation]{.red} |
| OS | [paging]{.green}, [interrupt handling]{.yellow}, [NUMA allocation]{.yellow}, [task scheduling]{.yellow}, [ASLR]{.yellow}, [noisy neighbors]{.yellow} |
| Runtime | [Allocator state]{.green}, [task scheduling]{.green} |

<style>
th {
    font-weight: bold;
}

.red {
    color: red
}

.yellow {
    color: orange
}

.green {
    color: green
}
</style>

---
layout: center
---

# **Solution**: Control as much as you can

- **disable**: SMT, DVFS, Power Saving, ...
- **pin**: core, NUMA, IRQ, ...
- **randomize everything else**: vmap/stack allocation, ...

---
layout: center
---

# Can we do better?

<style>
h1 {
    font-size: 5rem
}
</style>

---
layout: center
---

# ✅ Better solution

## Run **2 algorithms** you want to compare _simultaneously_.

By calculating [candidate]{.candidate}-[baseline]{.baseline}, most of the common mode noise will be _automatically eliminated_.

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

<!--
There is a hidden dynamic library behind every executable
-->

---
layout: image
image: /images/scheme.svg
backgroundSize: auto 90%
---

---
layout: center
---

# Conclusion

- computers were never designed to reproduce performance
- performance measurements are not i.i.d.
- compare apples to apples

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
- <nobr><mdi-web /> <a href="https://bazhenov.me/">https://bazhenov.me/</a></nobr>

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
