<script>
   
    import { getContext } from 'svelte';

    import MdKeyboardArrowUp from 'svelte-icons/md/MdKeyboardArrowUp.svelte'

    import { slide } from "svelte/transition";
    
    export let id = "0";

    export let title = "";
    
    export let subTitle = "";

    let isHovered = false;

    let isFocused = false;

    const active = getContext("context");
    
    $: isCurrentActive = $active === id;

    const onClickHandler = () => {
        if (isCurrentActive) {
            
            $active = "-1";
        } 
        else {
            
            $active = id;
        }


    }
</script>


<div 
class="
    border-gray-100 
    border-2 
    rounded-sm
    m-10
">

    <button 
    on:click={onClickHandler}
    on:mouseenter={() => isHovered = true}
    on:mouseleave={() => isHovered = false}
    on:focus={() => isFocused = true}
    on:blur={() => isFocused = false}
    class="flex text-left w-full focus:outline-none items-center p-4"
    class:bg-blue-100={isHovered || isFocused}
    class:border-blue-300={isFocused}
    class:border-4={isFocused}
    >
        <div class="w-full">
            <div class="
                font-bold 
                text-lg
                mb-1 
                transition 
                text-gray-700 
            "

                class:text-blue-400={isHovered || isFocused}>
                
                <span class="
                    border-b-2 
                    inline-block 
                    border-transparent
                    transition
                "
                    class:border-opacity-50={isFocused}
                    class:border-blue-300={isFocused}
                >
                    {title}  
                </span>    
            </div>
    
            {#if !!subTitle} 
                <div class="text-gray-400 text-sm">
                    {subTitle}
                </div>
            {/if}
        </div>

        <div class="
            w-8
            transform 
            transition
            text-gray-300 
        "
        class:rotate-180={isCurrentActive}
        class:text-blue-400={isHovered || isFocused}>
            <MdKeyboardArrowUp/>
        </div>
    </button>

    {#if isCurrentActive}
        <div class="px-4 pb-4 mt-4 bg-slate-200"
        transition:slide>
            <slot/>
        </div>
    {/if}
</div>