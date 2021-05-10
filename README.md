# Introduction
This playbook will run the crane PoC utility asynchronously against batches of namespaces until it has completed running against all namespaces listed.

# Usage
1. Copy `config.yml.example` to `config.yml`.
1. Edit `config.yml` with desired values.
1. Run `ansible-playbook crane-migration-playbook.yml`

# Options
- **crane_path**: Path to the directory that contains the crane binary. **Default**: `{{ playbook_dir }}`
- **download_crane**: Turn downloading the crane binary on or off. **Default**: `true`
- **batch_count**: The number of namespaces to export at once. **Default**: `10`
- **src_kubeconfig**: Path to the source cluster kubeconfig. **Default**: `undefined`
- **dst_kubeconfig**: Path to the destination cluster kubeconfig. **Default**: `undefined`
- **namespaces**: A list of namespaces to migrate. **Default**: `[robot-shop]`

# Additional Information
A starting point for listing namespaces in a convenient format might be:  
`oc get namespaces -o go-template='{{ range .items }}{{ "- " }}{{ .metadata.name }}{{"\n"}}{{ end }}'`

You will likely want to exclude namespaces such as `default`, `kube-*`, `openshift` and `openshift-*`.
