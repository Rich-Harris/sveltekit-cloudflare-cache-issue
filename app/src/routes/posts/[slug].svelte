<script context="module" lang="ts">
	import type { Load } from '@sveltejs/kit/types';

	export const load: Load = async ({ fetch, params }) => {
		try {
			const res = await fetch(`/posts/${params.slug}.json`, {
				credentials: 'omit'
			});
			const json = await res.json();

			return {
				status: 200,
				props: json,
				maxage: 60 * 60 * 24
			};
		} catch (error) {
			console.error(error);

			// return {
			// 	status: 500,
			// 	error
			// };

			return {
				props: {
					message: error.stack
				}
			};
		}
	};
</script>

<script lang="ts">
	export let message: string;
</script>

<h1>Post Detail Page</h1>
<pre>{message}</pre>
