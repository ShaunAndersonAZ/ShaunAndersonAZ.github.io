---
published: true
header:
  overlay_image: #/assets/images/rocky-mtns.jpg
  caption: #"[CC License](https://creativecommons.org)"
categories:
        #- Testing
---
I frequently install new Linux systems.  These are typically either RedHat, Centos or Ubuntu.  I want every system I log into to have a similar look and feel.  

Long ago I settled on OhMyZSH running the theme PowerLevel10K.  I created an ansible playbook to configure the system I installed to setup my terminal.

Here is the playbook content:
{% raw %}
```
---
  - name: Setup RH/Centos Systems
    hosts: localhost
    tasks:
    - name: Install zsh
      ansible.builtin.package:
        name: zsh
        state: present
      become: true

    - name: Set user shell to zsh
      ansible.builtin.user:
        name: "{{ user }}"
        shell: /bin/zsh
      become: true

    - name: Download ohmyzsh
      ansible.builtin.get_url:
        url: https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
        dest: "/home/{{ user }}/install.sh"
        mode: '0755'

    - name: Install ohmyzsh
      ansible.builtin.script:
        cmd: "/home/{{ user }}/install.sh"

    - name: Install PowerLevel10K
      ansible.builtin.git:
        repo: https://github.com/romkatv/powerlevel10k.git
        dest: "/home/{{ user }}/.oh-my-zsh/custom/themes/powerlevel10k"
        depth: 1

    - name: Download NerdFonts
      ansible.builtin.get_url:
        url: https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/Meslo.zip
        dest: "/home/{{ user }}/Meslo.zip"

    - name: Create temp directory
      ansible.builtin.file:
        path: "/home/{{ user }}/Meslo"
        state: directory
        mode: '0755'

    - name: Install font files
      ansible.builtin.unarchive:
        src: "/home/{{ user }}/Meslo.zip"
        dest: "/home/{{ user }}/Meslo"

    - name: Move font files to fonts directory
      ansible.builtin.copy:
        src: "/home/{{ user }}/Meslo"
        dest: /usr/share/fonts/Meslo
        owner: root
      become: true

    - name: Update .zshrc
      ansible.builtin.lineinfile:
        path: "/home/{{ user }}/.zshrc"
        insertafter: EOF
        line: "source /home/{{ user }}/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme"
```
{% endraw %}

If you are using WSL you may need to configure the terminal to include the Meslo fonts on Windows.

<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

