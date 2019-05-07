#include <stdio.h>
#include <stdlib.h>
#include "SDL/SDL.h"
#include <SDL/SDL_image.h>
int main()
{
    SDL_Surface *ecran1 =NULL;
    SDL_Surface *image =NULL,*personage=NULL/*,*personage2=NULL*/;
    SDL_Rect positionecran1,positionpersonage1;
    char pause;
    int continuer =1,curseur=1;
 
    SDL_Event event;
    
    image = SDL_LoadBMP("nature.bmp");
    personage=IMG_Load("detective.png");
    SDL_SetColorKey(personage, SDL_SRCCOLORKEY, SDL_MapRGB(personage->format, 255, 255, 255));
     SDL_Surface *ecran2 =NULL;
    SDL_Rect positionecran2,positionpersonage2;

   
    positionecran2.x=497;
    positionecran2.y=0;
    positionpersonage2.x=497;
    positionpersonage2.y=110;
    positionecran1.x=0;
    positionecran1.y=0;
    positionpersonage1.x=50;
    positionpersonage1.y=110;
    SDL_Init(SDL_INIT_VIDEO);
    ecran1 = SDL_SetVideoMode(994, 600, 24, SDL_HWSURFACE );
     ecran2 = SDL_SetVideoMode(994, 600, 24, SDL_HWSURFACE );
    while (continuer)
    {
     SDL_WaitEvent(&event);
        SDL_BlitSurface(image, NULL, ecran1, &positionecran1);
        SDL_BlitSurface(personage,NULL,ecran1,&positionpersonage1);
        SDL_BlitSurface(image, NULL, ecran2, &positionecran2);
        SDL_BlitSurface(personage,NULL,ecran2,&positionpersonage2);
        SDL_Flip(ecran2);
        SDL_Flip(ecran1);
        switch (event.type)
        {
        case SDL_QUIT:
            continuer=0;
            break;
        case SDL_KEYDOWN:
            switch (event.key.keysym.sym)
            {
            case SDLK_ESCAPE:
                continuer=0;
                break;
        case SDLK_UP:
                positionpersonage1.y=positionpersonage1.y-10;
        break;
        case SDLK_DOWN:
                positionpersonage1.y=positionpersonage1.y+10;
        break;
            case SDLK_RIGHT:
                positionpersonage1.x=positionpersonage1.x+20;
                break;
            case SDLK_LEFT:
                positionpersonage1.x=positionpersonage1.x-20;
                break;
       
            case SDLK_z:
                positionpersonage2.y=positionpersonage2.y-10;
        break;
        case SDLK_s:
                positionpersonage2.y=positionpersonage2.y+10;
        break;
            case SDLK_d:
                positionpersonage2.x=positionpersonage2.x+20;
                break;
            case SDLK_q:
                positionpersonage2.x=positionpersonage2.x-20;
                break;
    }
       			break;
        case SDL_MOUSEBUTTONUP:              
                   
           
                    positionpersonage1.x=event.button.x;
                    positionpersonage1.y=event.button.y;
                //SDL_BlitSurface(personage,NULL,ecran,&positionpersonage);
                                     
                                
                    break;
                    
        }
    }
 
    SDL_FreeSurface(image);
    SDL_FreeSurface(personage);
 
    return 0;
}
