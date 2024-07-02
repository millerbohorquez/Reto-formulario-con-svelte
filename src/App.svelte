
<script>
    import { createForm } from "svelte-forms-lib";

	let showMessage = false;

    const { form, errors, handleChange, handleSubmit } = createForm({
      initialValues: {
        
		first_name:"",
		last_name:"",
		email_address: "",
		query_type:"",
		message:"",
		consent:"",
      },
      validate: values => {
        let errs = {};
		if (values.first_name === "") {
          errs["first_name"] = "This field is required";
        }
		if (values.last_name === "") {
          errs["last_name"] = "This field is required";
        }
		if (values.email_address === "") {
			errs["email_address"] = "Please enter a valid email address";
		}
		if (values.query_type === "") {
          errs["query_type"] = "Please select a query type";
        }
		if (values.message === "") {
			errs["message"] = "This field is required";
		}
		if (values.consent === "") {
			errs["consent"] = "To submit this form, please consent to being contacted";
		}
        return errs;
      },
      onSubmit: () => {
        showMessage = true; 
        setTimeout(() => {
          showMessage = false; 
        }, 3000);
      }
    });

  </script>

<header>
	<div id="confirmationMessage"  style="{showMessage ? 'display: block;' : 'display: none;'}">
		<p>
			<svg xmlns="http://www.w3.org/2000/svg" width="20" height="21" fill="none" viewBox="0 0 20 21">
				<path fill="#fff"
					d="M14.28 7.72a.748.748 0 0 1 0 1.06l-5.25 5.25a.748.748 0 0 1-1.06 0l-2.25-2.25a.75.75 0 1 1 1.06-1.06l1.72 1.72 4.72-4.72a.75.75 0 0 1 1.06 0Zm5.47 2.78A9.75 9.75 0 1 1 10 .75a9.76 9.76 0 0 1 9.75 9.75Zm-1.5 0A8.25 8.25 0 1 0 10 18.75a8.26 8.26 0 0 0 8.25-8.25Z" />
			</svg>Message Sent!
		</p>
		<p>Thanks for completing the form. We'll be in touch soon!</p>
	</div>
</header>
<main>
	<div class="form-container">
		<form id="contactForm" on:submit={handleSubmit}>
			<p class="negrita">Contact Us</p>

			<div class="name-fields">
				<label for="first_name">First Name <span>*</span>
					<input type="text" id="first_name" name="first_name" class="first_name" on:change={handleChange} bind:value={$form.first_name}>
					{#if $errors.first_name}
      				<small>{$errors.first_name}</small>
    				{/if}
				</label>

				<label for="last_name">Last Name <span>*</span>
					<input type="text" id="last_name" name="last_name" class="last_name" on:change={handleChange} bind:value={$form.last_name}>
					{#if $errors.last_name}
      				<small>{$errors.last_name}</small>
    				{/if}
				</label>
			</div>

			<label for="email_address">Email Address <span>*</span></label>
			<input type="email" id="email_address" name="email_address" class="email_address" on:change={handleChange} bind:value={$form.email_address}>
			{#if $errors.email_address}
			  <small>{$errors.email_address}</small><br>
			{/if}

			<br>
			
			<label for="query_type">Query Type <span>*</span></label>
			<div class="radio-group">
				<label class="l1">
					<input type="radio" class="r1" name="query_type" value="general" on:change={handleChange} bind:group={$form.query_type}>
					<svg xmlns="http://www.w3.org/2000/svg" width="20" height="21" fill="none" viewBox="0 0 20 21">
						<path class="svg" fill="#0C7D69"
							d="M10 .75a9.75 9.75 0 1 0 9.75 9.75A9.76 9.76 0 0 0 10 .75Zm0 18a8.25 8.25 0 1 1 8.25-8.25A8.26 8.26 0 0 1 10 18.75Zm5.25-8.25a5.25 5.25 0 1 1-10.499 0 5.25 5.25 0 0 1 10.499 0Z" />
					</svg>
					General Enquiry
				</label>
				<label class="l2">
					<input type="radio" name="query_type" value="support" on:change={handleChange} bind:group={$form.query_type}>
					<svg xmlns="http://www.w3.org/2000/svg" width="20" height="21" fill="none" viewBox="0 0 20 21">
						<path class="svg" fill="#0C7D69"
							d="M10 .75a9.75 9.75 0 1 0 9.75 9.75A9.76 9.76 0 0 0 10 .75Zm0 18a8.25 8.25 0 1 1 8.25-8.25A8.26 8.26 0 0 1 10 18.75Zm5.25-8.25a5.25 5.25 0 1 1-10.499 0 5.25 5.25 0 0 1 10.499 0Z" />
					</svg>
					Support Request
				</label>
			</div>
			{#if $errors.query_type}
                <small>{$errors.query_type}</small><br>
            {/if}

			<label for="message">Message <span>*</span></label>
			<textarea id="message" name="message" class="message" rows="4" on:change={handleChange} bind:value={$form.message}></textarea>
			{#if $errors.message}
			  <small>{$errors.message}</small><br>
			{/if}
			<br>
			<div class="checkbox-group">
				<label>
					<input type="checkbox" name="consent" on:change={handleChange} bind:value={$form.consent}>
					<svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" fill="none" viewBox="0 0 18 18">
						<path class="svg" fill="#0C7D69"
							d="M16.5 0h-15A1.5 1.5 0 0 0 0 1.5v15A1.5 1.5 0 0 0 1.5 18h15a1.5 1.5 0 0 0 1.5-1.5v-15A1.5 1.5 0 0 0 16.5 0Zm-3.22 7.28-5.25 5.25a.748.748 0 0 1-1.06 0l-2.25-2.25a.75.75 0 1 1 1.06-1.06l1.72 1.72 4.72-4.72a.751.751 0 0 1 1.06 1.06Z" />
					</svg>
					I consent to being contacted by the team <span>*</span>
				</label>
				{#if $errors.consent}
			  		<br><small>{$errors.consent}</small>
				{/if}
			</div>

			<button type="submit" class="ver">Submit</button>
		</form>
	</div>
</main>

