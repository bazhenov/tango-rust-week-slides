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

<!--
Thank people & organizers.

I'm intrested in benchmarking. Rust great.

Introduce a novel way of measuring performance – PB and TANGO
-->

---
layout: full
---

# How do we measure performance?

```rust {3-5|2,6}
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
repeat algorithm in a loop, measure total time.

repeat process to build CI.

Fundamental problem with this code – to assume PERF is the same.
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


<!--
A lot of factors spanning several system levels.

Not anything under control. And also CLOUD.
-->
---
layout: center
---

# **Solution**: Control as much as you can

- **disable**: SMT, DVFS, Power Saving, ...
- **pin**: core, NUMA, IRQ, ...
- **randomize everything else**: vmap/stack allocation, ...
- **running benchmarks for longer**: may actually get things worse.

<!--
Control as much as you can, randomize anything else to create fair env.

Running benchmarks for longer?

It generally works, but it's not easy.

It's harder now that it was before.
-->

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

<!--
Never benchmark a single algorithm in isolation.

It's almost impossible to control environment tightly enough.
-->

---
layout: image
image: /images/img1.svg
backgroundSize: 90% 90%
---

<!--
same algorithm, same OS, same hardware.

The don't look alike, do they?

Computers were designed to reproduce the results of computations, not a performance.
-->

---
layout: image
image: /images/img2.svg
backgroundSize: 90% 90%
---

---
layout: statement
---

# ⏱️
# Performance is only <nobr>short-term</nobr> predictabile

<!--
Like a weather.

Leverage. Tango is designed to do that!
-->

---
layout: image
image: /images/vcs.svg
backgroundSize: 90% auto
---

<!--
2 binaries may be at a different times

Each binary contains benchmarks as well as runner. And the runner can load both executables in the same process memory.

There is a hidden dynamic library behind every executable.
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

<!--
it's almost impossible to separate algorithm performance from state of hardware and OS

benchmarks themselves might be the reason

benchmarking is easier when you compare apples to apples. You compare the same code in the same environment at the same time. One of the ways to do so is to compare 2 algorithms at the same time in the same environment. This way your benchmarks will be more stable and less susceptible to abrupt changes in performance without any meaningful changes to the code.
-->

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

<!--
Hope you will give it a try, and if you can please give some Feedback.

If you have any questions please find me in hall, I will be glad to have a chat.
-->
