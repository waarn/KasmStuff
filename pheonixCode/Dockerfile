FROM kasmweb/core-ubuntu-jammy:1.17.0
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME

######### Customize Container Here ###########

# Install Phoenix 4.0.3

RUN  wget https://github.com/phcode-dev/phoenix-desktop/releases/download/prod-app-v4.0.3/phoenix-code_4.0.3_amd64_linux_bin-GLIBC-2.35.tar.gz \
    && tar -xvf phoenix-code_4.0.3_amd64_linux_bin-GLIBC-2.35.tar.gz \
    && apt update \
    && cd phoenix-code \
    && apt install libgtk-3-0 libwebkit2gtk-4.0-37 -y \
    && apt install gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-tools gstreamer1.0-libav -y

# Custom Startup Script

RUN echo "/usr/bin/desktop_ready && /home/kasm-user/phoenix-code/phoenix-code &" > $STARTUPDIR/custom_startup.sh \
&& chmod +x $STARTUPDIR/custom_startup.sh

# Update for single app enviornment

RUN cp $HOME/.config/xfce4/xfconf/single-application-xfce-perchannel-xml/* $HOME/.config/xfce4/xfconf/xfce-perchannel-xml/
RUN cp /usr/share/backgrounds/bg_kasm.png /usr/share/backgrounds/bg_default.png
RUN apt-get remove -y xfce4-panel

#ENV KASM_RESTRICTED_FILE_CHOOSER=1
#COPY ./src/ubuntu/install/gtk/ $INST_SCRIPTS/gtk/
#RUN bash $INST_SCRIPTS/gtk/install_restricted_file_chooser.sh
#COPY ./src/ubuntu/install/close_browser_breakout_via_file_manager/ $INST_SCRIPTS/close_browser_breakout_via_file_manager/
#RUN bash $INST_SCRIPTS/close_browser_breakout_via_file_manager/replace_thunar_with_empty_script.sh

######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME

USER 1000