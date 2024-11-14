<template>
<header class="header">
    <div class="container">
    <div class="header-row">
        <div class="header-left">
        <div class="header-left-block">
            <div data-target="nav-menu" class="menu-btn _open-btn">
            <span></span>
            <span></span>
            <span></span>
            </div>
            <nav id="nav-menu" class="header-nav _menu">
                <ul class="header-list">

                    <li><a href="#" class="header-link">
                    <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M6.12512 2.62505L6.56263 1.75003L7.43765 1.31253L6.56263 0.875017L6.12512 0L5.68761 0.875017L4.81259 1.31253L5.68761 1.75003L6.12512 2.62505ZM2.18754 4.37509L2.91654 2.91681L4.37509 2.18754L2.91654 1.45827L2.18754 0L1.45854 1.45827L0 2.18754L1.45854 2.91681L2.18754 4.37509ZM11.8127 7.87515L11.0837 9.33342L9.62519 10.0627L11.0837 10.792L11.8127 12.2502L12.5417 10.792L14.0003 10.0627L12.5417 9.33342L11.8127 7.87515ZM13.7438 2.57665L11.4236 0.256489C11.253 0.0853142 11.029 0 10.8051 0C10.5811 0 10.3572 0.0853142 10.1863 0.256489L0.256489 10.1863C-0.0853142 10.5281 -0.0853142 11.0821 0.256489 11.4236L2.57665 13.7438C2.74755 13.9147 2.9715 14 3.19518 14C3.41913 14 3.64308 13.9147 3.81398 13.7438L13.7438 3.81371C14.0856 3.47245 14.0856 2.91818 13.7438 2.57665ZM9.8289 5.56347L8.43681 4.17137L10.8048 1.80336L12.1969 3.19545L9.8289 5.56347Z" fill="white"></path></svg>
                    Текст в изображение
                    </a></li>

                    <li><a href="#" class="header-link">
                    <svg viewBox="64 64 896 896" width="1em" height="1em" fill="white" aria-hidden="true"><path d="M551.5 490.5H521c-4.6 0-8.4 3.7-8.4 8.4V720c0 4.6 3.7 8.4 8.4 8.4h30.5c4.6 0 8.4-3.7 8.4-8.4V498.9c-.1-4.6-3.8-8.4-8.4-8.4zM477.3 600h-88.1c-4.6 0-8.4 3.7-8.4 8.4v23.8c0 4.6 3.7 8.4 8.4 8.4h47.6v.7c-.6 29.9-23 49.8-56.5 49.8-39.2 0-63.6-30.7-63.6-81.4 0-50.1 23.9-80.6 62.3-80.6 28.1 0 47.5 13.5 55.4 38.3l.9 2.8h49.2l-.7-4.6C475.9 515.9 434.7 484 379 484c-68.8 0-113 49.4-113 125.9 0 77.5 43.7 126.1 113.6 126.1 64.4 0 106-40.3 106-102.9v-24.8c0-4.6-3.7-8.3-8.3-8.3z"></path><path d="M854.6 288.6L639.4 73.4c-6-6-14.1-9.4-22.6-9.4H192c-17.7 0-32 14.3-32 32v832c0 17.7 14.3 32 32 32h640c17.7 0 32-14.3 32-32V311.3c0-8.5-3.4-16.7-9.4-22.7zM602 137.8L790.2 326H602V137.8zM792 888H232V136h302v216a42 42 0 0042 42h216v494z"></path><path d="M608.2 727.8h32.3c4.6 0 8.4-3.7 8.4-8.4v-84.8h87.8c4.6 0 8.4-3.7 8.4-8.4v-25.5c0-4.6-3.7-8.4-8.4-8.4h-87.8v-58.9h96.8c4.6 0 8.4-3.7 8.4-8.4v-26.8c0-4.6-3.7-8.4-8.4-8.4H608.2c-4.6 0-8.4 3.7-8.4 8.4v221.1c0 4.8 3.8 8.5 8.4 8.5z"></path></svg>
                    Текст в видео
                    </a></li>
                </ul>
            </nav>
        </div>
        <a href="#" class="header-left-logo">Insomnia Land</a>
        </div>
        <div class="header-rihgth">
            <img data-target="user-menu" src="https://insomnia.land/assets/avatar-3bcb50de.jpeg" alt="#" class="header-user-img _open-btn">
            <div id="user-menu" class="header-user-menu _menu">
                <a href="#" class="header-user-menu-link">Прайс</a>
                <span></span>
                <a href="#" class="header-user-menu-link">Telegram</a>
                <a href="#" class="header-user-menu-link">Discord</a>
                <span></span>
                <a href="#" class="header-user-menu-link">Русский</a>
            </div>
        </div>
    </div>
    </div>
</header>
</template>

<script>
export default {
    mounted() {
        // Функция для открытия/закрытия меню
        function toggleMenu(button) {
            const targetId = button.getAttribute('data-target'); // Получаем ID меню из data-атрибута
            const menu = document.getElementById(targetId); // Находим элемент меню по ID

            // Добавляем или удаляем класс '_open' для показа/скрытия меню
            if (menu) {
                menu.classList.toggle('_open');
            }
            document.addEventListener('click', function(e) {
            if(menu.closest('._open') && !e.target.closest('._menu') && !e.target.closest('._open-btn')) {
                menu.classList.remove('_open');
            }
            })
        }

        // Получаем все кнопки с классом '._open-btn'
        const buttons = document.querySelectorAll('._open-btn');

        // Назначаем обработчик события для каждой кнопки
        buttons.forEach(button => {
            button.addEventListener('click', () => toggleMenu(button));
        });
    },
}
</script>

<style lang="scss">
.header {
    padding: 13.5px 0;
}
.header-row {
    justify-content: space-between;
    display: flex;
    align-items: center;
}
.header-left {
    column-gap: 16px;
    display: flex;
    align-items: center;
}
.header-left-block {
    display: flex;
    align-items: center;
    column-gap: 16px;
    position: relative;
}
.menu-btn {
    width: 28px;
    height: 30px;
    position: relative;
    display: flex;
    z-index:2;
    overflow: hidden;
    cursor: pointer;
}
.menu-btn span {
    width: 28px;
    height: 2px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
    transition: all 0.5s;
}
.menu-btn span:nth-of-type(2) {
    top: calc(50% - 8px);
}
.menu-btn span:nth-of-type(3) {
    top: calc(50% + 8px);
}
.header-nav {
    background: #232323;
    width: 333px;
    position: absolute;
    top: 60%;
    left: 0;
    z-index: 3;
    padding: 14px;
    box-shadow: 0 8px 25px #00000029;
    border-radius: 14px;
    visibility: hidden;
    opacity: 0;
    transition: all .3s ease 0s;
}
.header-list {
    display: flex;
    flex-direction: column;
    row-gap: 4px;
}
.header-link {
    padding: 14px;
    display: flex;
    align-items: center;
    gap: 10px;
    border-radius: 10px;
    color: #fff;
    font-size: 14px;
    font-weight: 400;
    transition: all .3s ease 0s;
    &:hover {
    background-color: #ffffff0d;
    }
}
.header-left-logo {
    font-size: 16px;
    font-weight: 600;
    color: #fff;
}

.header-rihgth {
    position: relative;
}
.header-user-img {
    max-width: 36px;
    width: 100%;
    height: 36px;
    border-radius: 100%;
    cursor: pointer;
}
.header-user-menu {
    width: 160px;
    top: 100%;
    right: 0;
    position: absolute;
    padding: 14px;
    background: rgba(35, 35, 35);
    box-shadow: 0 8px 25px #00000029;
    border-radius: 10px;
    flex-direction: column;
    gap: 14px;
    display: inline-flex;
    visibility: hidden;
    opacity: 0;
    transition: all .3s ease 0s;
    & span {
        width: 100%;
        height: 1px;
        background: rgba(255, 255, 255, .1);
    }
}
.header-user-menu-link {
    font-weight: 400;
}
._open {
    visibility: visible;
    opacity: 1;
}
</style>