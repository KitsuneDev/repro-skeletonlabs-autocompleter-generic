<script lang="ts">
	import { getModalStore } from "@skeletonlabs/skeleton;"
	let modalStore = getModalStore();
	interface User {
		id: number;
		username: string;
		age: number;
	}

	// 1. Imagine we have a list of users...
	let user: User[] = [{id: 1, username: "Luna", 22}, {id: 2, username: "John", 24}];

	// 2. We can wrap them in AutocompleteOption<T>, where T = User...
	let autoCompletes = user.map(x=>{} satisfies AutocompleteOption<User>)





	function SubmitUser()


</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2 font-bold">Users</h2>
		<!-- Animated Logo -->
		</div>
</div>

<style lang="postcss">
	figure {
		@apply flex relative flex-col;
	}
	figure svg,
	.img-bg {
		@apply w-64 h-64 md:w-80 md:h-80;
	}
	.img-bg {
		@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
		animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,
			glow 5s linear infinite;
	}
	@keyframes glow {
		0% {
			@apply bg-primary-400/50;
		}
		33% {
			@apply bg-secondary-400/50;
		}
		66% {
			@apply bg-tertiary-400/50;
		}
		100% {
			@apply bg-primary-400/50;
		}
	}
	@keyframes pulse {
		50% {
			transform: scale(1.5);
		}
	}
</style>
