<script> 

    let title = "Starting with Svelte";

    let newItem;

    let todoItems = [		
        { id: 1, done: false, description: 'write some code' },
		{ id: 2, done: false, description: 'start writing working on zowned' },
		{ id: 3, done: true, description: 'buy some milk' },
		{ id: 4, done: false, description: 'mow the lawn' },
		{ id: 5, done: false, description: 'feed the turtle' },
		{ id: 6, done: false, description: 'fix some bugs' },
    ]

    function handleToggle (item){
        console.log("I'm inside handleToggle func - this is basically doing nothing since it doesn't re-render the todo items");
        // you gotta set the value of the binded prop to re-render
        // todoItems.find(each => {if(item.id === each.id) each.done = !each.done}) 
    }

    function addItem(){
        const newTodo = {
            id: todoItems.length,
            done: false,
            description: newItem
        };
        todoItems = [...todoItems, newTodo];
        newItem = "";
    }

    function removeItem(itemToRemove){
        todoItems = todoItems.filter(each => each.id !== itemToRemove.id);
    }

</script>

<style>
    .items{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-content: space-between;
        align-items: center;
    }
    #checkbox{
        margin: 0.5rem;
    }
    .description{
        margin-bottom: 0.1rem;
        border: 0rem;
        /* width: auto; */
    }
    .description:hover{
        border: 0.1rem solid #ccc;
    }
    .cross-icon{
        display: flex;
        align-items: flex-end;
        margin: 0.5rem;
        margin-bottom: 0.6rem;
        cursor: pointer;
        color: red;
        opacity: 0;
    }
    .items:hover .cross-icon{
        opacity: 1;
    }
    button{
        color: black;
        cursor: pointer;
        background-color: dodgerblue;
    }
    button:hover{
        background-color: black;
        color: dodgerblue; 
        border: 0.1rem solid black;
    }
</style>

<h2>{title} </h2>

<div>
    <input type="text" bind:value={newItem}/>
    <button on:click={addItem}>Add item</button>
</div>

<h3>To-do items</h3>
<div >
    {#each todoItems as item}
        {#if !item.done}
            <div class={"items"}>
                    <input type="checkbox" id={"checkbox"} bind:checked={item.done}/>
                    <input class={"description"} bind:value={item.description}/> 
                    <span class={"cross-icon"} title={"Click to remove item"} on:click={()=>removeItem(item)}> x </span>
            </div>
        {/if}
    {/each}
</div>

<br />

<h3>Completed Items</h3>
<div>
    {#each todoItems as item}
        {#if item.done}
            <div class={"items"}>
                    <input type="checkbox" id={"checkbox"} bind:checked={item.done}/>
                    <span class={"description"}>{item.description}</span>
                    <span class={"cross-icon"} title={"Click to remove item"}> x </span>
            </div>
        {/if}
    {/each}
</div>