<script lang="ts">
	import { Autocomplete, type AutocompleteOption } from "@skeletonlabs/skeleton";
	import { getModalStore } from "@skeletonlabs/skeleton";
	let modalStore = getModalStore();

	
	interface User {
		id: number;
		username: string;
		age: number;
	}

	// 1. Imagine we have a list of users...
	let user: User[] = [{id: 1, username: "Luna", age: 22}, {id: 2, username: "John", age: 24}];

	// 2. We can wrap them in AutocompleteOption<T>, where T = User...
	let autocompleteOptions = user.map(x=>({
		value: x,
		label: x.username
	}) satisfies AutocompleteOption<User>)


	let selectedValue: User | null;
	let inputValueRef: User | null; 
	// --> inputValueRef
	// This has to be user, even if we are input only deals with a string, because of how https://github.com/skeletonlabs/skeleton/blob/cb80c1624a0a0a5975fe29585caf95fc305ee0c4/packages/skeleton/src/lib/components/Autocomplete/Autocomplete.svelte#L38 is defined.
	// Even though it binds to an HTML input, which should only take a string.
	// My point is simply that:
	//    export let input: Value | undefined = undefined;
	// Should be: 
	//    export let input: string | undefined = undefined;

	function onSelected(x: CustomEvent<AutocompleteOption>){
		// In order to submit the user, we would need the whole object, in order to get ".id".
		// So to do this, we store it in `selectedUser`
		selectedValue = (x.detail.value as User);
		// To provide feedback to the user that it has been selected, we also update the input's text value.
		// However, since we CANNOT set the type of `inputValueRef` to `string`...
		inputValueRef = selectedValue.username as any as User; // We have to blatantly lie to Typescript.
	}


	function SubmitUser(){
		if(!selectedValue) {
			modalStore.trigger({
                title: "Invalid Selection",
                body: "Please select a valid option.",
                type: "alert"
            });
			return;
		}
		let userId = selectedValue!.id;
		// fetch() or whatever with `userId`
		modalStore.trigger({
                title: "Weee",
                body: `You selected user ${userId}`,
                type: "alert"
            });
			return;
	}
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2 font-bold">Users</h2>
		<input class="input" type="search" name="autocompleter" bind:value={inputValueRef} placeholder="Search..."/>
		<Autocomplete bind:input={inputValueRef} options={autocompleteOptions} on:selection={onSelected} />
		<button class="btn variant-filled" on:click={SubmitUser}>Submit</button>
		</div>
</div>
