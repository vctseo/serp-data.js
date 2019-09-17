(function() {
    clear();
    const urls = [];
    const titles = [];
    const descriptions = [];

    function uniq(value, index, self) { 
        return self.indexOf(value) === index;
    }
    
    const data = {};
    
    const u = '#rso > div > div > div > div > div > div.r > a';           
    let found = document.querySelectorAll(u);       

    if (found.length > 0) {
        found.forEach((f) => {
            let text = f.href;                                                           
            if (text) {
                urls.push(text);
            } else {
                urls.push("");
            }
        });
    }

    const t = '#rso > div > div > div > div > div > div.r > a > h3 > div';
    found = document.querySelectorAll(t);

    if (found.length > 0) {
        found.forEach((f) => {
            let text = f.textContent;                                                           
            if (text) {
                titles.push(text);
            } else {
                titles.push("");
            }
        });
    }

    const d = '#rso > div > div > div > div > div > div.s > div > span';
    found = document.querySelectorAll(d);

    if (found.length > 0) {
        found.forEach((f) => {
            let text = f.textContent;                                                           
            if (text) {
                descriptions.push(text);
            } else {
                descriptions.push("");
            }
        });
    }


    const range = n => Array.from(Array(n).keys());
    const result = [];

    for (const position of range(urls.length)) {
        const url = urls[position];
        const title = titles[position];
        const desc = descriptions[position];
        result.push(`${position+1}\t"${url}"\t"${title}"\t"${desc}"`);
    }

    const content = "position\turl\ttitle\tdescription\n" + result.join("\n");
    console.log(content);
})();
