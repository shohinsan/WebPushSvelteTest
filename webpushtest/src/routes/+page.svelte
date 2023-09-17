<script>
    import { onMount } from "svelte";
    import {Switch} from "@svelteuidev/core";

    let notificationsAlreadyEnabled = false;
    let notificationsDenied = false;

    function toggleNotification() {
        if (notificationsAlreadyEnabled) {
            notificationsAlreadyEnabled = false;
            console.log("Notifications disabled");
        } else {
            if (notificationsDenied) {
                console.log("Notifications are denied. You can't enable them.");
            } else {
                if (("Notification" in window)) {
                    Notification.requestPermission().then((result) => {
                        if (result === 'granted') {
                            console.log("Notifications enabled");
                            notificationsAlreadyEnabled = true;
                        } else if (result === 'denied') {
                            console.log("Notifications denied");
                            notificationsDenied = true;
                        }
                    });
                }
            }
        }
    }

    onMount(() => {
        notificationsAlreadyEnabled = Notification.permission === 'granted';
        notificationsDenied = Notification.permission === 'denied';
    });
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<Switch
        checked={notificationsAlreadyEnabled}
        size='md'
        onLabel="ON"
        offLabel="OFF"
        id="Notificationclick"
        on:click={() => {
        console.log('Notificationclick');
        toggleNotification();
    }}
/>


<!-- always Checked example -->

<br />
<br />

<Switch
        checked
        size='md'
        onLabel="ON"
        offLabel="OFF"
        id="Notificationclick"
/>
