# tauri-functions
Utility functions for tauri 


### Export File

```tsx
import { save } from "@tauri-apps/api/dialog";
import { writeFile } from "@tauri-apps/api/fs";



const SaveFile = async (filename: string, content: string, extension: string) => {
    const filepath = await save({
        defaultPath: filename,
        filters: [
          {
            name: filename,
            extensions: [extension],
          },
        ],
      });
      if (filepath) {
        await writeFile(filepath, content);
      }
}
```

### Copy to Clipboard

```tsx
import { writeText } from "@tauri-apps/api/clipboard";


const copyToClipboard = async (text: string) => {
  try {
    // Use the clipboard API to write text to the clipboard
    await writeText(text);
    // Optionally, you can notify the user that the text has been copied
    console.log("Text copied to clipboard:", text);
  } catch (error) {
    console.error("Error copying to clipboard:", error);
  }
};

```


### FileSize

```ts

export function bytesToSize(bytes: number): string {
  const sizes = ["Bytes", "KB", "MB", "GB", "TB"];
  if (bytes === 0) return "n/a";
  const i = Math.min(
    Math.floor(Math.log(bytes) / Math.log(1024)),
    sizes.length - 1
  );
  if (i === 0) return `${bytes} ${sizes[i]}`;
  return `${(bytes / 1024 ** i).toFixed(1)} ${sizes[i]}`;
}

const len = new TextEncoder().encode("File content").length;
console.log("size: ", bytesToSize(len));
```




