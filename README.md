Role Name
=========

This role can be used to obtain information from a running Kubernetes or OpenShift Cluster. The role will selectivly return data based on the input parameters passed in - including filtering using a json_query. 

Requirements
------------

Same as the [k8s_facts](https://docs.ansible.com/ansible/latest/modules/k8s_facts_module.html#requirements) Ansible Module.


Role Variables
--------------

**Input**

| Variable Name | Description | Required | Other Info |
| ------------- | ----------- | -------- | ---------- |
| openshift_get_resources.kind | The object to retrieve | Yes | |
| openshift_get_resources.name | Name of a specific object | No | |
| openshift_get_resources.namespace | The namespace where the object exists | No | |
| openshift_get_resources.api_version | API version for the object | No | |
| openshift_get_resources.ca_cert | Path to a CA cert used to authenticate with the API | No | |
| openshift_get_resources.client_cert | Path to a certificate used to authenticate with the API | No | |
| openshift_get_resources.client_key | Path to a key file used to authenticate with the API | No | |
| openshift_get_resources.validate_certs | Whether or not to verify the API server's SSL certs | No | |
| openshift_get_resources.host | URL for accessing the API | No | |
| openshift_get_resources.api_key | Token used to authenticate with the API | No | |
| openshift_get_resources.kubeconfig | Path to an existing kubernetes config file | No | Uses `~/.kube/config` by default |
| openshift_get_resources.context | Name of the context in the config file for the target API server | No | |
| openshift_get_resources.username | Username for when a token/pre-existing config file is *not* used | No | |
| openshift_get_resources.password | Password for when a token/pre-existing config file is *not* used | No | |
| openshift_get_resources.label_selectors | List of label selectors used to filter output | No | |
| openshift_get_resources.field_selectors | List of field selectors used to filter output | No | |
| openshift_get_resources.json_query | json_query used to filter output | No | This filter is built upon jmespath, and you can use the same syntax. For examples, see [jmespath examples](http://jmespath.org/examples.html). |

**Output**

| Variable Name | Description | Other Info |
| ------------- | ----------- | ---------- |
| openshift_get_resources.output | Where the output from the role is stored. | *Tip:* Use the json_query to limit the output to exact value. |

Dependencies
------------

N/A

Example Playbook
----------------

    - hosts: servers
      gather_facts: false
      vars:
        openshift_get_resources:
          kind: service
          namespace: default
          label_selectors:
            - router = router 
      roles:
         - role: openshift-get-resources

    - hosts: servers
      gather_facts: false
      vars:
        openshift_get_resources:
          kind: service
          namespace: default
          json_query: 'resources[*].metadata.annotations[]."openshift.io/scc"'
      roles:
         - role: openshift-get-resources

License
-------

Apache


Author Information
------------------
Øystein Bedin <oybed78@gmail.com>

