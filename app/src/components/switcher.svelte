<script>
    import { onMount } from "svelte";
    import {SunIcon , MoonIcon } from 'svelte-feather-icons';

    let scroll = false;

    onMount(() => {
        window.addEventListener("scroll", () => {
            scroll = window.scrollY > 50;
        });
    });

    const toggleTheme = () => {
        const htmlTag = document.getElementsByTagName("html")[0];
        htmlTag.classList.toggle("dark");
    };

    const toggleDirection = () => {
        const htmlTag = document.getElementsByTagName("html")[0];
        htmlTag.dir = htmlTag.dir === "ltr" ? "rtl" : "ltr";
    };

    const scrollTop = () => {
        window.scrollTo({ 
            top: 0,  
            behavior: 'smooth'
        });
    };
</script>

<a href="/#" on:click={()=>scrollTop()} id="back-to-top" class={`back-to-top fixed text-lg rounded-full z-10 bottom-5 right-5 size-9 text-center bg-teal-500 text-white leading-9 ${scroll ? 'block' : 'hidden' }`}><i class="mdi mdi-arrow-up"></i></a>

<div class="fixed top-1/4 -right-1 z-3">
    <span class="relative inline-block rotate-90">
        <input type="checkbox" class="checkbox opacity-0 absolute" id="chk" on:change={() => toggleTheme()} />
        <label class="label bg-slate-900 dark:bg-white shadow dark:shadow-gray-800 cursor-pointer rounded-full flex justify-between items-center p-1 w-14 h-8" for="chk">
            <SunIcon class="w-[18px] h-[18px] text-yellow-500"/>
            <MoonIcon class="w-[18px] h-[18px] text-yellow-500"/>
            <span class="ball bg-white dark:bg-slate-900 rounded-full absolute top-[2px] left-[2px] size-7"></span>
        </label>
    </span>
</div>

<div class="fixed top-[40%] -right-3 z-50">
    <a href={null} id="switchRtl" on:click={(event) => toggleDirection(event)}>
        <span class="cursor-pointer py-1 px-3 relative inline-block rounded-t-md -rotate-90 bg-white dark:bg-slate-900 shadow-md dark:shadow dark:shadow-gray-800 font-medium rtl:block ltr:hidden" >LTR</span>
        <span class="cursor-pointer py-1 px-3 relative inline-block rounded-t-md -rotate-90 bg-white dark:bg-slate-900 shadow-md dark:shadow dark:shadow-gray-800 font-medium ltr:block rtl:hidden">RTL</span>
    </a>
</div>
