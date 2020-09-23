<div align="center">

## EXE Header Info


</div>

### Description

Get .exe file header info
 
### More Info
 
a File to read header of.

outputs header info


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Shoots AndLadders](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/shoots-andladders.md)
**Level**          |Intermediate
**User Rating**    |4.7 (28 globes from 6 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__3-2.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/shoots-andladders-exe-header-info__3-830/archive/master.zip)

### API Declarations

stdio.h


### Source Code

```
#include <stdio.h>
struct EXEHEAD
{
	char id[2];				// 'M' & 'Z'
	unsigned lastpg;		// no of bytes on last page
	unsigned size;			// total no of 512 byte pages
	unsigned reloc;			// no of relocation table items
	unsigned headersize;	// header size in paras
	unsigned minpara;		// min. paras reqd. by prog.
	unsigned maxpara;		// max. paras reqd. by prog.
	unsigned stackseg;		// initial value of stack seg.
	unsigned stackoff;		// initial value of SP
	unsigned chksum;		// header check sum
	unsigned IP;			// entry point IP
	unsigned CS;			// entry point CS
	unsigned relocoff;		// offset of 1st relocation item
	unsigned char overlay;	// overlay number
};
int main(int argc, char *argv[])
{
	FILE *fp;
	struct EXEHEAD exehead;
	if((fp = fopen(argv[1], "rb")) == NULL)
	{
		printf("ERROR: file open error: %s\n", argv[1]);
		return 1;
	}
	fread(&exehead, sizeof(exehead), 1, fp);
	printf("EXE file signature: %c%c\n", exehead.id[0], exehead.id[1]);
	printf("Total bytes on last sectors: %u\n", exehead.lastpg);
	printf("Total sectors(1 sector = 512 bytes): %u\n", exehead.size);
	printf("No. of relocation table items: %u\n", exehead.reloc);
	printf("Header size in paragraphs: %u\n", exehead.headersize);
	printf("Min. paras. reqd. by program: %u\n", exehead.minpara);
	printf("Max. paras. reqd. by program: %u\n", exehead.maxpara);
	printf("Initial value of SS: %u\n", exehead.stackseg);
	printf("Initial value of SP: %u\n", exehead.stackoff);
	printf("Header checksum: %u\n", exehead.chksum);
	printf("Initial value of IP: %u\n", exehead.IP);
	printf("Initial value of CS: %u\n", exehead.CS);
	printf("Offset of 1st relocation item: %u\n", exehead.relocoff);
	printf("Overlay number: %d\n", exehead.overlay);
	return 0;
}
```

