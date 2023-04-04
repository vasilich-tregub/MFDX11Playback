# MF Playback with DX11VideoRenderer Sink

Based off Windows Desktop Wizard, Desktop Application project template with CPlayer class 
from Media Session Playback Example added 
(see https://learn.microsoft.com/en-us/windows/win32/medfound/media-session-playback-example), 
the sample demonstrates the use of DX11VideoRenderer sink in a Media Session topology for 
video playback.

Changes are made 
to the CPlayer class, mostly to the CreateMediaSinkActivate method;
to the DX11VideoRenderer sample: in the method 
DX11VideoRenderer::CPresenter::SetXVPOutputMediaType(...), the initial VideoWindow dimensions are set 
to the display dimensions (width x height). The method originally called MFInitVideoFormat_RGB with 
m_rcDstApp which to the moment of execution is set to the original window size. As the result of this 
setting, the video window cannot be zoomed in greater than the original video window size.

After restoring a minimized window of the player, the video hangs (the audio continues unimpeded). 
As a temporary remedy, I removed a minimize option of the window menu. Also, I restricted the 
minimum size of the video window.

With the display adapter feature level below D3D_FEATURE_LEVEL_11_0, the performance of this 
configuration is lower than with the EVR presenter. 

TODO: to discover what prevents the renderer from presenting the samples after window minimization;
examine if the diminished performance is the flaw of this implementation, where it is located (in 
CPlayer or in DX11VideoRenderer), and what can be a remedy, if any.
