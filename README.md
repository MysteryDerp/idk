# i dont like github (im still learning) and this is really minimalistic xd (and yes... i didnt follow a youtube tutorial for this little creation of mine) and FUCK windows
```
#include <iostream>
#include <Windows.h>
#include <getbaseaddress.h>
#include <Csleep.h>

using namespace std;

DWORD procID;
HWND hwnd;
int pointer, DLLbase;
const int offset0 = 11129052, offset1 = 45732, Aoffset = 49005116;
int address, Aaddress;
int crosshair;
bool state = false;
bool check = true;
int shoot;


int main()
{
	hwnd = FindWindowA(NULL, "Counter-Strike: Global Offensive");
	if (hwnd == NULL)
	{
		cout << "cannot find CSGO window. make sure you have CSGO open\n";
		system("pause");
		return -1;
	}
	GetWindowThreadProcessId(hwnd, &procID);
	HANDLE handle = OpenProcess(PROCESS_ALL_ACCESS, FALSE, procID);
	while (!GetAsyncKeyState(VK_INSERT))
	{
		if (state)
		{
			ReadProcessMemory(handle, (LPVOID)address, &crosshair, sizeof(crosshair), 0);
			if (crosshair > 0 && crosshair < 64)
			{
				shoot = 5;
				WriteProcessMemory(handle, (LPVOID)Aaddress, &shoot, sizeof(shoot), 0);
				Csleep(50);
				shoot = 4;
				WriteProcessMemory(handle, (LPVOID)Aaddress, &shoot, sizeof(shoot), 0);
				Csleep(50);
			}
			else
			{
				if (GetAsyncKeyState(VK_F1))
				{
					Beep(523, 500); // 523 hertz (C5) for 500 milliseconds     
					state = !state;
					while (GetAsyncKeyState(VK_F1));
				}
			}
		}
		else
		{
			
			DLLbase = GetModuleBase(procID, (TCHAR*)"client.dll");
			pointer = DLLbase + offset0;
			ReadProcessMemory(handle, (LPVOID)pointer, &pointer, sizeof(pointer), 0);
			address = pointer + offset1;
			Aaddress = DLLbase + Aoffset;
			if (GetAsyncKeyState(VK_F1))
			{
				Beep(523, 500); // 523 hertz (C5) for 500 milliseconds     
				Beep(523, 500); // 523 hertz (C5) for 500 milliseconds     
				state = !state;
				while (GetAsyncKeyState(VK_F1));
			}
			Sleep(50);
		}

			if (state)
			{
				system("cls");
				cout << "cheat is ON... toggle by F1 or close the cheat by INSERT!\nNOTE: to close the cheat you HAVE to click INSERT";
			}
			else
			{
				system("cls");
				cout << "cheat is OFF... toggle by F1 or close the cheat by INSERT!\nNOTE: to close the cheat you HAVE to click INSERT";
			}
	}
	CloseHandle(handle);
    return 0;
}
```



