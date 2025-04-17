Classic WordPress Theme – Tailwind CSS 4 + Pinegrow (inspired by Adam Lowe’s course)

Hey folks! Just wanted to share a classic WordPress theme I’ve been working on, built using Pinegrow and the latest Tailwind CSS v4. This project was inspired by Adam Lowe’s excellent WordPress theme course, which he very generously made free on YouTube — big thanks to Adam!

What’s different from the original course?
	•	Instead of vanilla CSS, I rebuilt the whole theme using Tailwind CSS (v4) and UI blocks from Tailwind UI.
	•	Skipped the contact form implementation — for most projects, Contact Form 7 or any free form plugin will integrate better and faster.
	•	CPTs and taxonomies were created directly using functions.php and ChatGPT (faster for me than Pinegrow in this case)* see code
	•	Custom blocks and layouts are done with Pinegrow’s WordPress features + Tailwind utility classes.
	•	The search form title is different to that of Adamn tutorial. I just injected the php:  <h2 class="text-3xl font-bold mb-8">
    Search Results for: <span class="text-red-600"><?php echo esc_html( get_search_query() ); ?></span></h2>

 

Included Templates:
	•	404.html – includes a working search module
	•	archive-employees.html
	•	blocks.html – houses reusable blocks (used some on homepage)
	•	customizer.html
	•	index.html
	•	parts.html – partials used throughout theme
	•	search.html
	•	single-employee.html
	•	single.html
	•	utilities.html – general utility classes/helpers

Menu functionality:
	•	Responsive nav is working in both desktop and mobile view.
	•	I couldn’t get submenus working properly yet — gave it my best shot! Anyone who wants to take a look or improve it is totally welcome.

Why it might help others:

If you’re exploring Tailwind + Pinegrow + WordPress and looking for a classic (non-FSE) theme structure, this could be a helpful starting point. Especially if you’re transitioning from traditional theme dev into a utility-first workflow.

Would love feedback or improvements from the community — happy to share the repo or a ZIP if anyone’s interested.

Cheers!

* feel free to to download and use as you please. 
* /* CPT and Taxonomy */

<code>
function create_employee_post_type() {
    register_post_type('employee',
        array(
            'labels' => array(
                'name' => __('Employees'),
                'singular_name' => __('Employee'),
                // ... other labels ...
            ),
            'public' => true,
            'has_archive' => true,
            'rewrite' => array('slug' => 'employees'),
            'supports' => array('title', 'editor', 'custom-fields', 'thumbnail'), // ✅ Add 'thumbnail' here
            'show_in_rest' => true,
        )
    );
}
</code>
<code>
function create_department_taxonomy() {
    register_taxonomy('department', 'employee', array(
        'labels' => array(
            'name' => __('Departments'),
            'singular_name' => __('Department'),
            'search_items' => __('Search Departments'),
            'all_items' => __('All Departments'),
            'parent_item' => __('Parent Department'),
            'parent_item_colon' => __('Parent Department:'),
            'edit_item' => __('Edit Department'),
            'update_item' => __('Update Department'),
            'add_new_item' => __('Add New Department'),
            'new_item_name' => __('New Department Name'),
            'menu_name' => __('Departments'),
        ),
        'hierarchical' => true,
        'rewrite' => array('slug' => 'department'),
        'show_in_rest' => true,
    ));
}

add_action('init', 'create_employee_post_type');
add_action('init', 'create_department_taxonomy');

/* End CPT and Taxonomy */
</code>
