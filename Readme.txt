 <span style={styles.infoValStyle} title={
                        activePass
                            ? `${activePass.passConfig || (selectedSat?.defaultPassConfig || 'Yok')} / ${activePass.endingConfig || (selectedSat?.defaultEndingConfig || 'Yok')}`
                            : 'Konfigürasyon Yok'
                    }>
                        {activePass
                            ? `${activePass.passConfig || (selectedSat?.defaultPassConfig || (lang === 'tr' ? 'Varsayılan Yok' : 'No Default'))} / ${activePass.endingConfig || (selectedSat?.defaultEndingConfig || (lang === 'tr' ? 'Varsayılan Yok' : 'No Default'))}`
                            : (lang === 'tr' ? 'Geçiş Konfigürasyonu Yok / Geçiş Sonu Konfigürasyonu Yok' : 'No Pass Config / No Ending Config')}
