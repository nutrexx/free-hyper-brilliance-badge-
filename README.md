```js
(async () => {
    try {
        const webpackRequire = webpackChunkdiscord_app.push([
            [Symbol("hypesquad")],
            {},
            (require) => require,
        ]);

        webpackChunkdiscord_app.pop();

        const modules = webpackRequire.m;
        const cache = webpackRequire.c;

        function findByCode(source) {
            for (const [id, mod] of Object.entries(modules)) {
                if (typeof mod === "function" && mod.toString().includes(source)) {
                    return cache[id]?.exports;
                }
            }
            return undefined;
        }

        function findObjectFromKey(exports, key) {
            if (!exports) return undefined;

            for (const value of Object.values(exports)) {
                if (value && typeof value === "object" && key in value) {
                    return value;
                }
            }

            return undefined;
        }

        const moduleExports = findByCode(
            '.set("X-Audit-Log-Reason",'
        );

        const api = findObjectFromKey(moduleExports, "patch");

        if (!api || typeof api.post !== "function") {
            console.error("Could not locate the expected API module.");
            return;
        }

        console.log("API module found. Sending request...");

        const response = await api.post({
            url: "/hypesquad/online",
            body: { house_id: 2 },
        });

        console.log("Request completed:", response);
    } catch (error) {
        console.error("Request failed:", error);
    }
})();
```
