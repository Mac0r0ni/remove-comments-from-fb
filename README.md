# remove-comments-from-fb
Remove comments from facebook profile.

FB allows you to see all of your past comments. You may want to clear them out. 
  
Find your FB tag -- your tag is the part after facebook.com in the url when you go to your profile.

Go to this URL (replace YOURTAGHERE with the tag found above): https://www.facebook.com/YOURTAGHERE/allactivity?entry_point=www_top_menu_button&privacy_source=activity_log&log_filter=cluster_116&category_key=commentscluster
  
Hit f12 to open the developers console, and then hit Console.  
  
Drop this piece of code into the console:  

```javascript
function get_rid_of_em() {
    window.scrollBy(0, 10000) 

    const elements = document.querySelectorAll('[aria-label="Action options"]') // Or insert the classname you find in your inspector!
    for (const idx in elements) {
        try {
            elements[idx].click()
        } catch(e) {
            console.log(e)
        }
    }

    const deletes = document.querySelectorAll('[role="menuitem"]') // Or insert the classname you find in your inspector!
    for (const idx in deletes) {
        try {
            deletes[idx].click()
        } catch(e) {
            console.log(e)
        }
    }
}

setInterval(get_rid_of_em, 0.1)
```

https://www.facebook.com/YOURTAGHERE/allactivity/?activity_history=true&category_key=ALL&manage_mode=false&should_load_landing_page=false

```javascript
function automateClicks() {
    // Define the XPaths for the elements
    const xpath1 = "/html/body/div[1]/div/div[1]/div/div[3]/div/div/div[1]/div[1]/div[2]/div/div/div/div/div/div[2]/div[2]/div/div[2]/div/i";
    const xpath2 = "/html/body/div[1]/div/div[1]/div/div[3]/div/div/div[2]/div/div/div[1]/div[1]/div/div/div/div/div/div/div[1]/div/div/div[2]/div/div/span";
    const xpath3 = "/html/body/div[1]/div/div[1]/div/div[4]/div/div/div[1]/div/div[2]/div/div/div/div/div/div/div[3]/div/div/div/div/div[1]/div/div";

    // Helper function to find an element by XPath
    function getElementByXPath(xpath) {
        return document.evaluate(xpath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
    }

    // Function to simulate the clicking process
    function clickSequence() {
        // Click the first element
        const element1 = getElementByXPath(xpath1);
        if (element1) element1.click();

        // Wait 0.8 seconds, then click the second element
        setTimeout(() => {
            const element2 = getElementByXPath(xpath2);
            if (element2) element2.click();
        }, 800);

        // Wait another 0.8 seconds (1.6 seconds total), then click the third element
        setTimeout(() => {
            const element3 = getElementByXPath(xpath3);
            if (element3) element3.click();
        }, 1600);
    }

    // Function to repeat the click sequence every 2 seconds after the clicks
    function repeatSequence() {
        clickSequence();
        setTimeout(repeatSequence, 2000); // Repeat the sequence every 2 seconds
    }

    // Start the automation
    repeatSequence();
}

// Run the automation
automateClicks();
```


Note that the class names may change may change.  
To fix this, replace those classnames by right clicking on the element on the screen that you want to click,  
hit 'Inspect Element' (which should go to the elements tab of the dev console), and look for 'class=X'. 

Also note that there may be an error window that shows the text 'Could not complete query'. Ignore it. It's just due to new comments not being totally loaded in yet. The script will keep working, regardless. At some point you should probably refresh to make sure the comments are actually being deleted, it doesn't show up otherwise.
