MAKEING C# LOADER FOR PASTE CLICKERS 😎😎
![image](https://user-images.githubusercontent.com/70253785/155404754-e360d0be-1bab-46a6-bdce-ae2ddea00470.png)

#include <iostream>
 
#include <Windows.h>
#include <thread>
 
void loop()
{
    HWND hwnd;
    do
    {
        hwnd = FindWindow(L"LWJGL", NULL);
        if (hwnd) break;
 
        std::this_thread::sleep_for(std::chrono::seconds(1));
    } while (true);
 
    std::cout << "Found HWND, ready to click.\n";
 
    bool toggled = false;
    while (true)
    {
        // This is your toggle key. Default: VK_TAB
        if ((GetKeyState(VK_TAB) & 0x100))
        {
            toggled = !toggled;
 
            std::cout << (toggled ? "Toggled" : "Disabled") << std::endl;
 
            std::this_thread::sleep_for(std::chrono::seconds(1));
 
            if (!toggled) continue;
        }
 
        if (toggled && (GetKeyState(VK_LBUTTON) & 0x100))
        {
            PostMessage(hwnd, WM_LBUTTONUP, MK_LBUTTON, 0);
 
            PostMessage(hwnd, WM_LBUTTONDOWN, MK_LBUTTON, 0);
            // Change the 88 to a higher or lower number to lower or increase the DPS. Default: 88 ms
            std::this_thread::sleep_for(std::chrono::milliseconds(88));
        }
    }
}
 
int main()
{
    std::thread(loop).join();
    return 0;
}
