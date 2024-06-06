
    <ul>
        <li><a href="#" onclick="showTab('linux')">Linux</a></li>
        <li><a href="#" onclick="showTab('windows')">Windows</a></li>
        <li><a href="#" onclick="showTab('macos')">MacOS</a></li>
    </ul>

    <div id="linux" class="tab-content">
        Contenido para Linux.
    </div>

    <div id="windows" class="tab-content">
        Contenido para Windows.
    </div>

    <div id="macos" class="tab-content">
        Contenido para MacOS.
    </div>

    <script>
        function showTab(tabName) {
            var tabs = document.querySelectorAll('.tab-content');
            tabs.forEach(function(tab) {
                tab.classList.remove('active');
            });

            var tabToShow = document.getElementById(tabName);
            tabToShow.classList.add('active');
        }
    </script>