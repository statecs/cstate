<template src="./AppListTemplate.html"></template>

<script>
import AppHeader from "./AppHeader.vue";
// Import methods and data
import dataContent from './AppListData.json';

export default {
  name: "AppList",
  props: {
    msg: String
  },
  components: {
    AppHeader
  },
  computed: {
    isMobileDevice() {
      return /Android|webOS|iPhone|iPad|iPod|BlackBerry|Windows Phone/i.test(navigator.userAgent);
    }
  },
  methods: {
    addScrollListener: function(id, handler) {
        const element = document.getElementById(id);
        if (element) {
            element.addEventListener("scroll", handler);
        } else {
            console.warn(`Element with ID ${id} not found when trying to add scroll listener.`);
        }
    },

    expandCard: function(event, index) {
    var el = event.currentTarget; 
    var body = document.body;

    // Check if the clicked card is already active
    if (this.transitionIndex === index && this.transitioning) {
        // Logic to collapse the card...
        this.transitionIndex = -1;  // or another value indicating no card is active
        this.removeFocusTrap(el);
        console.log("click to close");
    } else {
        // Logic to expand the card...
        this.transitionIndex = index;
    }

     // Store the previously focused element
     this.previousActiveElement = document.activeElement;

    // Logging for debugging
    console.log("Device:", this.isMobileDevice ? "Mobile" : "Non-Mobile");
    
    if (!this.isMobileDevice) {

      if (el.style.transform && el.style.transform !== "translateY(0px)") {
        // If there's a transform applied, and it's not the default, reset it.
        el.style.transform = "translateY(0px)";
      } else {
        var distanceToTop = el.getBoundingClientRect().top;
        console.log("Initial distanceToTop:", distanceToTop);  // Log initial value

        if (distanceToTop < 0) {
          // If the element is already above the viewport, reset the transform
          //el.style.transform = "translateY(0px)";
          el.style.transform = "translateY(" + -distanceToTop + "px)";
          console.log("Element above viewport. Resetting transform.");
        } else {
          distanceToTop = -1 * distanceToTop;
          console.log("Adjusted distanceToTop:", distanceToTop);  // Log adjusted value

          // Fix: Ensure distanceToTop is set to 0 if it's an unexpected value.
          if (Math.abs(distanceToTop) > window.innerHeight) {
            distanceToTop = 0;
            console.warn("Unexpected distanceToTop value. Resetting to 0.");
          }

          el.style.transform = "translateY(" + distanceToTop + "px)";
        }
      }
    } else {
      body.classList.toggle("mobile-scroll");
    }

    setTimeout(() => {
        this.transitionIndex = index;
        if (this.transitioning) {
          this.setFocusTrap(el);
        } else {
          this.removeFocusTrap(el);
        }
      }, 200);
      
      this.transitioning = !this.transitioning;
      body.classList.toggle("no-scroll");
    },
    
    setFocusTrap: function(element) {
      const focusableElements = 'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])';
      const focusable = Array.from(element.querySelectorAll(focusableElements));

      if (focusable.length > 0) {
        focusable[0].focus();
      }

      element.addEventListener('keydown', this.trapFocus.bind(this, focusable));
    },
    trapFocus: function(focusable, event) {
      const firstElement = focusable[0];
      const lastElement = focusable[focusable.length - 1];

      if (event.key === 'Tab' && event.shiftKey) {
        if (document.activeElement === firstElement) {
          event.preventDefault();
          lastElement.focus();
        }
      } else if (event.key === 'Tab') {
        if (document.activeElement === lastElement) {
          event.preventDefault();
          firstElement.focus();
        }
      }
    },
    removeFocusTrap: function(element) {
    console.log("Removing focus trap", { element });
    if (element) {
        element.removeEventListener('keydown', this.trapFocus);
        
        // Log and check previousActiveElement
        console.log("Previous active element: ", this.previousActiveElement);
        console.log("Is focusable: ", !!this.previousActiveElement.focus);
        
        if (this.previousActiveElement) {
            try {
                this.previousActiveElement.focus();
            } catch (error) {
                console.error("Error focusing on previousActiveElement: ", error);
                
                // Fallback: set focus to a stable element if previousActiveElement fails
                document.body.focus(); 
            }
        }
    } else {
        console.warn("Element is not available in removeFocusTrap");
    }

  }
  
  },
  data: function() {
  return {
    ...dataContent,
    previousActiveElement: null
  };
},

mounted: function() {
    this.addScrollListener("scroll-1", this.updateScroll1);
    this.addScrollListener("scroll-2", this.updateScroll2);
    this.addScrollListener("scroll-3", this.updateScroll3);
},

};
</script>

<style scoped>
@import '../assets/AppListStyles.css';
</style>
