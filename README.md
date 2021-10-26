# Ansible-snipets-
My compilation of useful Ansible code snippets.

# Using a Default Variable

~~~yml
# register the output of a command to a variable called result. Then debug the variable to the console. 
- name: Run CreatePolicyVersion Shadow admin Priv Esc 
  shell: <command>
  register: result

- debug:
    msg: '{{ result.stdout }}'
~~~

# JSON Manipulation and Formatting

~~~yml
- name: Query json object & assign to variable
   - set_fact: Var='{{ result.stdout | from_json | json_query("Key") }}'

- name: More complex query(slicing). Real life AWS IAM example. 
   - set_fact: PublicIpAddress='{{ result2.stdout | from_json | json_query("Reservations") | json_query("[0]") | json_query("Instances") | json_query("[0]") | json_query("NetworkInterfaces") | json_query("[0]") | json_query("Association") | json_query("PublicIp") }}'

- name: Simple debug.
  debug:
    msg: "{{ simple_value }}"

- name: Get foo value.
  set_fact:
    foo_value: "{{ (json.stdout | from_json).example_list | map(attribute='foo') | list }}"

- name: Jinja list debug, printing out the list as comma seperated.
  debug:
    msg: "{% for each in foo_value %}{{ each }}{% if not loop.last %},{% endif %}{% endfor %}"
~~~
