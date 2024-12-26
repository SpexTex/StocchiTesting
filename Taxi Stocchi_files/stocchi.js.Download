document.addEventListener("DOMContentLoaded", () => {
    console.log("DOM fully loaded and parsed");

    let lastScrollTop = 0;
    const topBar = document.querySelector('.top-bar');
    const header = document.querySelector('header');
    const burgerMenu = document.querySelector('.burger-menu');
    const navLinks = document.querySelector('.nav-links');

    // Create overlay element
    const overlay = document.createElement('div');
    overlay.className = 'menu-overlay';
    document.body.appendChild(overlay);

    // Toggle menu function
    function toggleMenu() {
        burgerMenu.classList.toggle('active');
        navLinks.classList.toggle('active');
        overlay.classList.toggle('active');
        document.body.style.overflowY = navLinks.classList.contains('active') ? 'hidden' : 'auto';
    }

    // Event Listeners
    burgerMenu.addEventListener('click', toggleMenu);
    overlay.addEventListener('click', toggleMenu);

    // Close menu when clicking a nav link
    navLinks.querySelectorAll('a').forEach(link => {
        link.addEventListener('click', () => {
            navLinks.classList.remove('active');
            burgerMenu.classList.remove('active');
            overlay.classList.remove('active');
            document.body.style.overflowY = 'auto';
        });
    });

    // Scroll handling
    window.addEventListener('scroll', () => {
        const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
        if (scrollTop > lastScrollTop) {
            topBar.classList.add('hidden');
            header.classList.add('top-bar-hidden');
        } else {
            topBar.classList.remove('hidden');
            header.classList.remove('top-bar-hidden');
        }
        lastScrollTop = scrollTop <= 0 ? 0 : scrollTop; // For Mobile or negative scroll positions
    });

    // Hero section responsive handling
    const hero = document.querySelector('.hero');
    const heroImg = hero.querySelector('img');
    const heroText = document.querySelector('.hero-text');
    
    // Function to handle hero section scaling
    function handleHeroScaling() {
        const windowWidth = window.innerWidth;
        const windowHeight = window.innerHeight;
        
        // Adjust hero height based on screen orientation and size
        if (windowWidth <= 480) {
            hero.style.height = windowHeight < 600 ? '50vh' : '60vh';
        } else if (windowWidth <= 768) {
            hero.style.height = windowHeight < 1024 ? '60vh' : '70vh';
        } else {
            hero.style.height = '80vh';
        }

        // Fix hero text position to always stay in the same spot
        heroText.style.top = '23%';
        heroText.style.left = '23%';
        heroText.style.transform = 'translate(-50%, -50%)';
    }

    // Parallax effect for hero image
    function handleParallax() {
        if (window.innerWidth) { 
            const scrolled = window.pageYOffset;
            heroImg.style.transform = `translateY(${scrolled * 0.5}px)`;
        } else {
            heroImg.style.transform = 'translateY(0)'; // Reset transform on smaller screens
        }
    }

    // Handle text visibility on scroll
    function handleTextVisibility() {
        const scrolled = window.pageYOffset;
        const heroHeight = hero.offsetHeight;
        
        if (scrolled < heroHeight) {
            const opacity = 1 - (scrolled / heroHeight * 1.5);
            heroText.style.opacity = Math.max(opacity, 0);
        } else {
            heroText.style.opacity = 1; // Ensure text remains visible after scrolling past hero section
        }
    }


 // Smooth scroll to specific sections
 document.querySelectorAll('.nav-links a, .footer-column a').forEach(link => {
    link.addEventListener('click', function (e) {
        const targetText = this.textContent.trim().toLowerCase();
        let targetElement;

        // Map text content to section classes
        if (targetText === 'kontakt') {
            targetElement = document.querySelector('.contact-form-section');
        } else if (targetText === 'dienstleistungen') {
            targetElement = document.querySelector('.services');
        }

        // Perform the smooth scroll if target is found
        if (targetElement) {
            e.preventDefault();
            const offset = -95; // Adjust this value if needed
            const targetPosition = targetElement.getBoundingClientRect().top + window.pageYOffset + offset;
            window.scrollTo({ top: targetPosition, behavior: 'smooth' });
        }
    });
    });

    // Event listeners
    window.addEventListener('resize', handleHeroScaling);
    window.addEventListener('scroll', () => {
        handleParallax();
        handleTextVisibility();
    });
    window.addEventListener('orientationchange', handleHeroScaling);
    
    // Initial setup
    handleHeroScaling();
});
